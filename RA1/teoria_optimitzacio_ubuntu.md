# Teoria: Optimització del Sistema en Ubuntu

## 1. Introducció
L’optimització del sistema operatiu té com a objectiu millorar el rendiment general d’Ubuntu, reduir el consum de recursos i assegurar que la màquina funcioni de manera fluida. Aquest procés implica analitzar l’ús de CPU, memòria, disc i serveis, i aplicar canvis per reduir càrrega i temps d’arrencada.

## 2. Monitorització del Rendiment

### 2.1 CPU
La CPU és un recurs essencial i els processos que s’executen poden consumir gran quantitat de cicle de processador.

Comandes habituals:
- `top` o `htop` → mostra en temps real els processos i ús de CPU.
- Processos amb més consum poden indicar programes mal optimitzats o serveis innecessaris.

### 2.2 Memòria RAM
La RAM emmagatzema informació temporal dels programes actius.

Comandes útils:
- `free -h` → mostra memòria total, lliure i swap.
- L’ús elevat de swap pot indicar manca de RAM o massa aplicacions obertes.

### 2.3 Disc i Inodes
L'espai en disc i el nombre d’inodes també afecten el rendiment.

- `df -h` → ús del disc.
- `df -i` → ús d’inodes.

Si un disc està ple, Ubuntu pot alentir-se o fallar en iniciar serveis.

## 3. Serveis del Sistema i Temps d'Arrencada

### 3.1 systemd i analitzadors
Ubuntu utilitza systemd per gestionar l’arrencada.

- `systemd-analyze time` → mostra el temps total d’arrencada.
- `systemd-analyze blame` → mostra quins serveis triguen més.

Aquestes dades permeten detectar serveis que podrien ser desactivats per millorar el temps d’arrencada.

## 4. Optimització del Sistema

### 4.1 Eliminació de Programari Innecessari
Amb el temps, el sistema acumula paquets no utilitzats.

Ordres útils:
- `sudo apt remove --purge paquet`
- `sudo apt autoremove`
- `sudo apt clean`

Eliminar programari allibera espai i pot reduir càrrega del sistema.

### 4.2 Gestió de Serveis
Ubuntu inicia diversos serveis per defecte. Alguns no són necessaris segons l’ús de la màquina.

- Llistar serveis:
  `systemctl list-unit-files --type=service`
- Desactivar un servei:
  `sudo systemctl disable nom_servei`

Desactivar serveis innecessaris pot reduir consum de RAM i velocitzar l’arrencada.

## 5. Rendiment del Disc

### 5.1 Anàlisi d’Ocupació
Algunes carpetes poden ocupar molt espai.

- `ncdu` → eina interactiva per analitzar el disc.

### 5.2 TRIM per SSD
Els SSD necessiten TRIM per mantenir el rendiment amb el temps.

- `sudo systemctl enable fstrim.timer`
- `sudo systemctl start fstrim.timer`

TRIM ajuda a que el disc SSD netegi blocs no utilitzats i mantingui la seva velocitat original.

## 6. Conclusions
Optimitzar Ubuntu és un procés gradual que inclou:
- Diagnosi del rendiment.
- Eliminació de programari prescindible.
- Gestió de serveis del sistema.
- Optimització del disc.
- Revisió periòdica de recursos.

Aquest conjunt de pràctiques permet mantenir el sistema estable, ràpid i preparat per a l’ús diari o entorns educatius i professionals.
