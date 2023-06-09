<table align="center">
  <tr>
    <td align="center">
      <h1>NeoPixel</h1>
    </td>
  </tr>
</table>

<p align="center">
  <img src="https://media.printables.com/media/prints/424552/images/3513078_8d1e1e1d-9b91-4a44-b07d-d7ec10c436a1/thumbs/cover/1200x630/jpg/img_20230314_112653.jpg" width="50%">
</p>


<br>

---
**Configuration des Neopixels:**
---

<br>
<br>
Pour configurer les Néopixels dans Klipper, vous aurez besoin de définir les paramètres appropriés dans la section [neopixel] de votre fichier de configuration. <br>
<br>
Tout d'abord, vous pouvez donner un nom personnalisé à vos Néopixels en utilisant le paramètre 'pin'. Assurez-vous de spécifier le numéro de broche du microcontrôleur auquel sont connectés vos Neopixels.
<br>
<br>
Ensuite, vous pouvez indiquer combien de Néopixels sont connectés en série à la broche fournie en utilisant le paramètre 'chain_count'. 
<br>
<br>
L'ordre des couleurs des pixels doit également être spécifié avec le paramètre 'color_order', qui est généralement GRB, mais peut également être RGB ou RGBW en fonction du matériel LED que vous utilisez.
<br>
<br>
Enfin, vous pouvez définir les valeurs initiales des composantes de couleur rouge, vert, bleu et blanc du Neopixel en utilisant les paramètres 'initial_RED', 'initial_GREEN', 'initial_BLUE' et 'initial_WHITE'. Dans cet exemple, les valeurs sont mises à 0.0 pour éteindre les Neopixels au démarrage.
<br>
<br>

```
[neopixel name_neopixel]
  # Vous pouvez mettre le nom que vous 
  # souhaitez à vos Néopixels

pin:
  # Numéro de broche du microcontrôleur 
  # auquel est connecté le Neopixel (obligatoire).

chain_count:
  # Nombre de Neopixels connectés en série 
  # à la broche fournie.

color_order: GRB
  # Ordre des couleurs des pixels requis par
  # le matériel LED (par défaut: GRB) 
  # RGB, RGBW peuvent être mis.

initial_RED: 0.0
initial_GREEN: 0.0
initial_BLUE: 0.0
initial_WHITE: 0.0
  # Valeurs initiales des composantes de couleur
  # rouge, vert, bleu et blanc du Neopixel.
  # Dans ce cas elles sont éteintes.
```
<br>
Ceci doit être inclus dans un fichier que l'on peux nommer "Neopixel.cfg".<br>
Ensuite il vous faudrat l'inclure dans votre printer.cfg avec ceci: <br>

```
[include Neopixel.cfg]
```

<br>

On va maintenant aller voir [ici](https://github.com/Eloura74/NeoPixel/blob/main/Variables.md) pour définir les différentes variables.
<br>
