# CockroachDB - Cnam

## Installer un client

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



## Cluster CockroachDB - Exercice
<br>

- Déployer un cluster CockroachDB avec 3 nodes<br>
- Vérifier qu'il fonctionne correctement<br>
- Créer une base de données<br>
- Ajouter une table<br>
- Insérer des données dans cette table<br>
- Accéder aux données de cette table depuis chacun des 3 containers<br>
- Explorer la console d'administration<br>
- Faire tomber un node et vérifier le comportement (connexion, requête, console, logs...)<br>

Requête sql pour créer une table avec un autoincrement.
```shell
cockroach sql --database=mynewdb --execute="CREATE TABLE person (id serial, firstname varchar(255));" --insecure
```

Requête sql pour insérer des data dans cette table
```shell
cockroach sql --database=mynewdb --execute="INSERT INTO person (firstname) SELECT md5(random()::text) 
FROM generate_series(1, 5);" --insecure --echo-sql
```

## [CockroachDB single node - step01](step01/step01.md)

## [CockroachDB two nodes - step02](step02/step02.md)

## [CockroachDB three nodes - step03](step03/step03.md)

## [CockroachDB three nodes and loadbalancer - step04](step04/step04.md)

## Initialiser le cluster

```shell
cockroach init --insecure --cluster-name=cockroach-cluster
```
## Workload MOVR

Initialisation du workload
```shell
cockroach workload init movr --help
```

Exécution du workload
```shell
cockroach workload run movr --help
```

Exécution du workload - exemple
```shell
cockroach workload run movr --duration=30s 'postgresql://root@localhost:26257?sslmode=disable'
```

```shell
cockroach workload run movr --duration=10s --num-vehicles=100 'postgresql://root@localhost:26257?sslmode=disable'
```



## [CockroachDB three nodes + load balancer + monitoring - step05](step05/step05.md)

In this case, you have to change Host IP in file  grafana/provisioning/datasources/datasource.yml   
```shell
url: http://host_ip_address:9090
```