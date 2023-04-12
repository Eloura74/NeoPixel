<table align="center">
  <tr>
    <td align="center">
      <h1>Installation</h1>
    </td>
  </tr>
</table>

<br>

![image](https://media.printables.com/media/prints/424552/images/3513078_8d1e1e1d-9b91-4a44-b07d-d7ec10c436a1/thumbs/cover/1200x630/jpg/img_20230314_112653.jpg)
<br>
**Commencer par vérifier et installer les mises à jour sur votre Raspberry Pi:**<br>
<br>
*Taper la commande :*
<br>
```
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```
**Maintenant on va installer le Module "Klipper Led_effect":**<br>
<br>
*Taper les commandes suivantes:*<br>
<br>
On va tout d'abord nous déplacer dans le répertoire personnel de l'utilisateur:
```
cd ~
```
Ensuite cette commande clône un dépôt Git depuis GitHub. Elle crée une copie locale du dépôt "klipper-led_effect" dans le répertoire courant:
```
git clone https://github.com/julianschill/klipper-led_effect.git
```
Une fois que le dépôt a été cloné avec succès, cette commande permet de se positionner dans le répertoire cloné:
```
cd klipper-led_effect
```
On va maintenant utiliser cette commande pour exécuter le script d'installation:
```
./install-led_effect.sh
```

**Ensuite on va integrer les mises à jour dans "Mooraker.conf":**<br>
<br>
*Ajouter ceci:*
<br>
```
[update_manager led_effect]
type: git_repo
path: ~/klipper-led_effect
origin: https://github.com/julianschill/klipper-led_effect.git
is_system_service: False
```

Voilà c'est tout pour l'installation. <br>
Il nous faut maintenant configurer les [Neopixels](https://github.com/Eloura74/NeoPixel/blob/main/Neopixel.md).
