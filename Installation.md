Commencer par vérifier et installer les mises à jour sur votre Raspberry Pi.
Taper la commande :
```
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```
Maintenant on va installer le Module "Klipper Led_effect":
Taper la commande:
```
cd ~
git clone https://github.com/julianschill/klipper-led_effect.git
cd klipper-led_effect
./install-led_effect.sh
```

Ensuite on va integrer les mises à jour dans "Mooraker.conf":
Ajouter ceci:
```
[update_manager led_effect]
type: git_repo
path: ~/klipper-led_effect
origin: https://github.com/julianschill/klipper-led_effect.git
is_system_service: False
```
