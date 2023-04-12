![image](https://media.printables.com/media/prints/424552/images/3513078_8d1e1e1d-9b91-4a44-b07d-d7ec10c436a1/thumbs/cover/1200x630/jpg/img_20230314_112653.jpg)
Commencer par vérifier et installer les mises à jour sur votre Raspberry Pi.<br>
Taper la commande :
```
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```
Maintenant on va installer le Module "Klipper Led_effect":<br>
Taper la commande:
```
cd ~
git clone https://github.com/julianschill/klipper-led_effect.git
cd klipper-led_effect
./install-led_effect.sh
```

Ensuite on va integrer les mises à jour dans "Mooraker.conf":<br>
Ajouter ceci:
```
[update_manager led_effect]
type: git_repo
path: ~/klipper-led_effect
origin: https://github.com/julianschill/klipper-led_effect.git
is_system_service: False
```

Voilà c'est tout pour l'installation. Il ne vous reste plus qu'à configurer les Néopixels.
