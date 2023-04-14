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
