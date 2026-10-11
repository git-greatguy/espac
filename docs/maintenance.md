# Maintenance et validation

Le protocole UART, l'encodage Airton, les actions du thermostat et les controles sont dans `packages/core.yaml`. Modifier cette seule source pour les corrections communes.

`home_assistant_edition/espac_configuration.yaml` ajoute Wi-Fi, API chiffree et OTA. Sans serveur web ni sonde Home Assistant obligatoire, il utilise la sonde interne comme auparavant.

`examples/personal.yaml` ajoute une sonde HA et le serveur web. C'est un exemple anonymise : conserver localement les identifiants, secrets, valeurs persistantes et entetes de la configuration personnelle avant migration. Il ne remplace pas automatiquement le firmware personnel teste. La presentation web est simplifiee (sans groupes de tri).

L'edition Wi-Fi v1.0.0 et son binaire historique restent inchanges. Leur mise a jour est hors de cette revision ; ils ne consomment pas encore le socle commun. Aucune nouvelle source Wi-Fi n'est publiee.

## Demarrage

Trois trames RX consecutives avec les memes reglages sont requises ; la temperature n'est pas comparee. A environ une trame par minute, cela peut prendre trois minutes. Les commandes UART sont bloquees jusque-la. Le thermostat peut afficher une demande qui n'est pas encore appliquee physiquement.

Apres synchronisation, une commande explicite API/web autorise le profil public a reprendre avec ses autres valeurs restaurees. Il ne force plus FAN_ONLY au boot. Le profil personnel avec `wait_complete_control: "true"` exige la reception du mode ET des deux bornes apres boot/resync. Il ne reconnait pas l'identite de Node-RED : toute commande ClimateCall correspondante peut fournir ces champs.

Le message � Pilotage externe pret � signifie que les gardes sont levees, pas que la PAC a confirme la commande. La divergence de consigne sur trois trames est un diagnostic sans renvoi automatique.

## Sonde HA optionnelle

Ajouter `external_sensor: !include ../packages/homeassistant-sensor.yaml` dans packages, puis les substitutions `ambient_sensor: external_temp` et `external_temperature_entity: sensor.your_room_temperature`. Adapter les chemins si le YAML est deplace. Le maintien de la derniere valeur HA n'est pas une garantie de fraicheur.

## Reglages conserves

Encodage entier Airton 16..31 �C, troncature conservee ; ecart de sondes 3 �C. Plage visuelle thermostat 16..34 �C. Les hysteresis persistantes peuvent remplacer les valeurs declarees : le source historique conserve les initial_value a 1 et les bases thermostat 0/0,5 en chauffe ; le reglage personnel 0,3/0,3 est un essai local, pas un defaut universel.

## Limites connues

Validation RX encore fondee sur la taille minimale et quelques valeurs ; pas de CRC RX. Transitions de commandes parfois multiples, comportement de sonde distante perimee et volets horizontaux inchanges. Les temporisations thermostat limitent les demandes ESPHome, pas les decisions internes du compresseur.

## Verification

Compiler les deux profils avec la version de requirements.txt. Pour les essais/CI uniquement, utiliser une copie du fichier secrets.yaml.example dans le dossier de chaque profil. Ne pas flasher ces valeurs d'exemple.

La configuration personnelle monolithique a compile et a ete essayee le 11 octobre 2026 : OFF au boot, resync puis FAN_ONLY demande pendant l'attente et applique apres 2 min 55 s. Le reboot pendant chauffe n'a pas ete teste. La factorisation et la variante publique de deverrouillage ne sont pas encore validees sur appareil.

Les fichiers images/, 3d_case/, .github/FUNDING.yml, wifi_edition/ et les releases existantes doivent etre conserves lors de l'application de cette revision.
