# Installer un client

Installation en local de la CLI cockroachDB

Script powershell a exécuter<br>
Télécharge CockroachDB et ajoute le dossier dézippé au PATH<br>
```shell
$ErrorActionPreference = "Stop"
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$ProgressPreference = 'SilentlyContinue'
$null = New-Item -Type Directory -Force $env:appdata/cockroach
Invoke-WebRequest -Uri https://binaries.cockroachdb.com/cockroach-v22.2.7.windows-6.2-amd64.zip -OutFile cockroach.zip
Expand-Archive -Force -Path cockroach.zip
Copy-Item -Force "cockroach/cockroach-v22.2.7.windows-6.2-amd64/cockroach.exe" -Destination $env:appdata/cockroach
$Env:PATH += ";$env:appdata/cockroach"
```

Ajouter cockroach au PATH
```
$Env:PATH += ";$env:appdata/cockroach"
```



# Cluster CockroachDB - Exercice
<br>

- Déployer un cluster CockroachDB avec 3 nodes<br>
- Vérifier qu'il fonctionne correctement<br>
- Créer une base de données<br>
- Ajouter une table<br>
- Insérer des données dans cette table<br>
- Accéder aux données de cette table depuis chacun des 3 containers<br>
- Explorer la console d'administration<br>
- Faire tomber un node et vérifier le comportement (connexion, requête, console, logs...)<br>
