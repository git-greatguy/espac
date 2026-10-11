# Unreleased

- Sources ESPAC publiees sous GPL-3.0-only (choix confirme par l'auteur).
- Protocole et regulation regroupes dans un package commun au profil API et a l'exemple personnel.
- Reprise des reglages Airton apres trois trames coherentes ; attente d'une commande utilisateur avant reprise du pilotage.
- Profil personnel : attente du mode et des deux bornes fraiches ; consigne UART derivee non reutilisee comme consigne de confort.
- Emission UART bloquee avant initialisation, sans ecriture de buffer vide.
- Diagnostic de divergence RX accessible, sans boucle de retransmission.
- Conservation des ameliorations du source personnel : flottants, encodage borne 16..31, minuterie millis et traduction Turbo.
- Edition Wi-Fi et binaire v1.0.0 inchanges.
