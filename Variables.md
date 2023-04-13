<p align="center">
  <img src="https://media.printables.com/media/prints/424552/images/3513078_8d1e1e1d-9b91-4a44-b07d-d7ec10c436a1/thumbs/cover/1200x630/jpg/img_20230314_112653.jpg" width="50%">
</p>

<table align="center">
  <tr>
    <td align="center">
      <h1>Variables</h1>
    </td>
  </tr>
</table>


<br>
Ces variables sont utilisées pour définir les couleurs associées à différents états ou modes de fonctionnement d'un éclairage pour une buse ou d'un logo Z dans un code de commande numérique. 
<br>
<br> 
Chaque état ou mode a une couleur associée définie en utilisant les valeurs de rouge (r), vert (g), bleu (b), et blanc (w) dans une échelle de 0 à 1 pour chaque composante de couleur. 
<br>
<br>
Les variables permettent de définir les couleurs utilisées dans le code de manière claire et modifiable.<br>
<br>
<br>
Il vous faudras créer un nouveau fichier que l'on nommera "Variables_led.cfg" et l'inclure dans votre printer.cfg
<br>
<br>


```
[include Variable_led.cfg]
```

```
[gcode_macro _sb_vars]

variable_colors: {

 # Différentes couleur du logo Z
        'logo': {
            'busy': {'r': 0.8, 'g': 0.0, 'b': 0.0, 'w': 0.0},
            'cleaning': {'r': 0.0, 'g': 0.02, 'b': 0.5, 'w': 0.0},
            'calibrating_z': {'r': 0.8, 'g': 0., 'b': 0.35, 'w': 0.0},
            'heating': {'r': 0.3, 'g': 0.18, 'b': 0.0, 'w': 0.0},
            'homing': {'r': 0.0, 'g': 0.6, 'b': 0.2, 'w': 0.0},
            'leveling': {'r': 0.5, 'g': 0.1, 'b': 0.4, 'w': 0.0},
            'meshing': {'r': 0.2, 'g': 1.0, 'b': 0.0, 'w': 0.0},
            'off': {'r': 0.0, 'g': 0.0, 'b': 0.0, 'w': 0.0},
            'on': {'r': 1.0, 'g': 1.0, 'b': 1.0, 'w':0.0},
            'printing': {'r': 1.0, 'g': 0.0, 'b': 0.0, 'w': 0.0},
            'standby': {'r': 0.01, 'g': 0.01, 'b': 0.01, 'w': 0.0},
        },
# Différentes couleur de la buse
        'nozzle': { 
            'heating': {'r': 0.8, 'g': 0.35, 'b': 0.0, 'w':0.0},
            'off': {'r': 0.0, 'g': 0.0, 'b': 0.0, 'w': 0.0},
            'on': {'r': 1.0, 'g': 1.0, 'b': 1.0, 'w':0.0}, 
            'standby': {'r': 0.6, 'g': 0.0, 'b': 0.0, 'w':0.0},
            'print': {'r': 0.8, 'g': 0.8, 'b': 0.8, 'w':0.0},
        },
# Couleur en fonction Température:
        'thermal': {
            'hot': {'r': 1.0, 'g': 0.0, 'b': 0.0, 'w': 0.0},
            'cold': {'r': 0.3, 'g': 0.0, 'b': 0.3, 'w': 0.0}
        },
    }
####################################################################

# Noms des differentes Variables:

# Le nom de la chaîne de LED adressables qui contient le(s) logo(s) LED.
variable_logo_led_name:         "sb_leds" 

# Numéro des LED séparés par des virgules dans le logo.
variable_logo_idx:              "1" 

# Le nom de la chaîne de LED adressables qui contient la ou les LED de la buse.
variable_nozzle_led_name:       "sb_leds"
 
# Numéro des LED séparés par des virgules dans la buse.
variable_nozzle_idx:            "2,3"

# Températures auxquelles le refroidissement sera considéré comme complet:
variable_thermal_config: {
        'extruder': {
            'cool_temp': 40,
            'leds': 'logo',
        },
        'heater_bed': {
            'cool_temp': 50,
            'leds': 'nozzle',
        },
    }

######################################## ATTENTION NE PAS TOUCHER ######################################## 
############################################## Ci-Dessous ################################################ 
gcode:

[gcode_macro _set_sb_leds]
gcode:
    # Définition de la variable red à partir du paramètre RED (rouge) avec une valeur par défaut de 0 et convertie en nombre flottant
    {% set red = params.RED|default(0)|float %}  
    # Définition de la variable green à partir du paramètre GREEN (vert) avec une valeur par défaut de 0 et convertie en nombre flottant
    {% set green = params.GREEN|default(0)|float %} 
    # Définition de la variable blue à partir du paramètre BLUE (bleu) avec une valeur par défaut de 0 et convertie en nombre flottant
    {% set blue = params.BLUE|default(0)|float %}  
    # Définition de la variable white à partir du paramètre WHITE (blanc) avec une valeur par défaut de 0 et convertie en nombre flottant
    {% set white = params.WHITE|default(0)|float %}  
    # Définition de la variable led à partir du paramètre LED (nom de la LED) et convertie en chaîne de caractères
    {% set led = params.LED|string %}  
    # Définition de la variable idx à partir du paramètre IDX (index de la LED) en le séparant par des virgules et convertie en liste de chaînes de caractères
    {% set idx = (params.IDX|string).split(',') %}  
    # Définition de la variable transmit_last à partir du paramètre TRANSMIT (transmission) avec une valeur par défaut de 1
    {% set transmit_last = params.TRANSMIT|default(1) %}  

    # Boucle pour chaque élément dans la liste idx
    {% for led_index in idx %}  
        # Si c'est le dernier élément de la liste, transmit prend la valeur de transmit_last, sinon elle prend la valeur 0
        {% set transmit=transmit_last if loop.last else 0 %}  
        # Commande gcode pour définir la couleur de la LED en fonction des variables définies précédemment
        set_led led={led} red={red} green={green} blue={blue} white={white} index={led_index} transmit={transmit}  
    {% endfor %}

[gcode_macro _set_sb_leds_by_name]
gcode:
    # Définition de la variable leds_name à partir du paramètre LEDS (nom de la LED)
    {% set leds_name = params.LEDS %}  
    # Définition de la variable color_name à partir du paramètre COLOR (nom de la couleur)
    {% set color_name = params.COLOR %}  
    # Définition de la variable color en accédant à un dictionnaire de couleurs spécifié par les variables leds_name et color_name
    {% set color = printer["gcode_macro _sb_vars"].colors[leds_name][color_name] %}  
    # Définition de la variable led en accédant à une variable spécifiée par la variable leds_name
    {% set led = printer["gcode_macro _sb_vars"][leds_name + "_led_name"] %}  
    # Définition de la variable idx en acc
    {% set idx = printer["gcode_macro _sb_vars"][leds_name + "_idx"] %}  


```

On va ensuite pouvoir passer à la création des différents [effets et macros](https://github.com/Eloura74/NeoPixel/blob/main/EffetsLed.md)
