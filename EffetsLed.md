<table align="center">
  <tr>
    <td align="center">
      <h1>Configuration des différents effets</h1>
    </td>
  </tr>
</table>


<p align="center">
  <img src="https://media.printables.com/media/prints/424552/images/3513078_8d1e1e1d-9b91-4a44-b07d-d7ec10c436a1/thumbs/cover/1200x630/jpg/img_20230314_112653.jpg" width="50%">
</p>

<br>

Vous devez ajouter un nouveau fichier pour pouvoir mettre tout les effets que vous aller créer. On peux le nommer "EffetsLed.cfg". <br>
On l'inclus ensuite au printer.cfg: <br>

```
[include EffetsLed.cfg]
```

<br>

<tr>
    <td align="center">
      <h1>Partie ON/OFF</h1>
    </td>
  </tr>
<br>


```
# Logo OFF/ON:

[gcode_macro Logo_off]
description: Logo Off
gcode:
    {% set transmit=params.TRANSMIT|default(1) %}
    _set_logo_leds red=0 blue=0 green=0 white=0 transmit={transmit}

[gcode_macro Logo_on]
description: Logo On
gcode:
    {% set transmit=params.TRANSMIT|default(1) %}
    _set_logo_leds red=0 blue=0.8 green=0 white=0 transmit={transmit}
    
###########################################################################                
# Nozzle OFF/ON:

[gcode_macro Buse_on]
description: Buse On
gcode:
    {% set transmit=params.TRANSMIT|default(1) %}
    _set_sb_leds_by_name leds="nozzle" color="on" transmit={transmit} 
    
[gcode_macro Buse_off]
description: Buse Off
gcode:
    {% set transmit=params.TRANSMIT|default(1) %}
    _set_sb_leds_by_name leds="nozzle" color="off" transmit={transmit}

###########################################################################
# Extinction TOTALE:

[gcode_macro status_off]
description: Eteindre toutes les Leds
gcode:
    STOP_LED_EFFECTS
    Logo_off
    Buse_off
    
###########################################################################
# Arrêter les effets:
[gcode_macro effects_off]
description: Arret de tout les effets
gcode:
    STOP_LED_EFFECTS
    
```
<tr>
    <td align="center">
      <h1>Exemple pour un statut lors du mesh:</h1>
    </td>
  </tr>
<br>


```
[gcode_macro status_meshing]
description: la buse est blanche et le logo est orange
gcode:
    _set_sb_leds_by_name leds="logo" color="meshing" transmit=0
    set_nozzle_leds_on

```
<tr>
    <td align="center">
      <h1>Extinction des Leds au bout d'un certain temps:</h1>
    </td>
  </tr>
<br>

Mettre STOP_EFFECT_DURATION à la fin de votre START_PRINT.

```
[delayed_gcode STOP_EFFECT_DURATION]
# description: Arret de toutes les lumières apres 300 sec. A mettre dans le Start_Gcode
initial_duration: 300.
gcode:
    STOP_LED_EFFECTS
    Logo_off
    Buse_off
    
```
<tr>
    <td align="center">
      <h1>Exemple d'effet de dégradé Bleu:</h1>
    </td>
  </tr>
<br>


```
# Effet rainbow bleu sur logo:
[led_effect chauffe_logo]
leds:
    neopixel:sb_leds (1)                    # Cela spécifie les LEDs à utiliser pour l'effet, en utilisant un modèle de LEDs appelé "neopixel:sb_leds" avec les                                                   # numéros de LED spécifiés entre parenthèses.
autostart:                          false   # Cela indique que l'effet ne doit pas démarrer automatiquement lors de l'exécution du code
frame_rate:                         24      # Cela définit la fréquence de rafraîchissement de l'effet à 24 images par seconde.
layers:
    gradient  0.3  1 add (0.0, 0.2, 0.5),(0.0, 0.8, 0.0),(0.0, 0.2, 0.8)
    # Cela définit les couches de l'effet, dans cet ordre : une couche de gradient avec une opacité de 0,3 et un mélange d'addition, avec trois couleurs définies en       # RGB : (0.0, 0.2, 0.5), (0.0, 0.8, 0.0), et (0.0, 0.2, 0.8). Cette combinaison de couleurs crée un effet de dégradé bleu
    
# Macro :
[gcode_macro chauffe_logo]
description: Effet bleu logo
gcode:
    STOP_LED_EFFECTS
    SET_LED_EFFECT EFFECT=chauffe_logo
    
```
<tr>
    <td align="center">
      <h1>On peux demander une couleur spécifique à une certaine température :</h1>
    </td>
  </tr>
<br>


```
[led_effect bed_hot]
leds:
    neopixel:sb_leds (1)                         # Choix des LEDS                     
autostart:                          true         # Cela indique que l'effet doit démarrer automatiquement lors de l'exécution du code
frame_rate:                         24           # Définit la fréquence d'allumage par seconde pour l'effet
heater:                             heater_bed   # Choisisser quelle valeur est prise en compte pour déclancher l'effet (heater_bed / extruder)   
layers:  
     heater  30.00 0 top   (0.04,0.04,1.00,0.00)

```

**Vous trouverez plus d'information sur la page [officiel](https://github.com/julianschill/klipper-led_effect/blob/master/docs/LED_Effect.md) du site pour avoir d'autres rendus.**
