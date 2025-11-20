# Exercici de Sistemes Operatius en Ubuntu
## Optimització del Sistema

## Objectiu
Analitzar el rendiment del sistema, detectar colls d’ampolla i aplicar millores d’optimització en un Ubuntu Desktop o Server.

## Materials necessaris
- Una màquina Ubuntu (real o virtual)
- Terminal
- Accés sudo

## Part 1 — Diagnosi del sistema

### 1. Monitorització de CPU
Executa:
```
top
```
Respon:
- Quins processos consumeixen més CPU?
- Quin percentatge de CPU lliure tens?

### 2. Monitorització de memòria RAM
Executa:
```
free -h
```
Respon:
- Quanta memòria total tens?
- Quanta està lliure?
- Ubuntu està fent ús de SWAP?

### 3. Ús del disc i inodes
Executa:
```
df -h
df -i
```
Respon:
- Quines particions estan a punt d’omplir-se?
- Hi ha alguna partició amb pocs inodes disponibles?

### 4. Servei que s’ha iniciat més lentament
Executa:
```
systemd-analyze blame
```
Respon:
- Quin servei triga més a arrancar?
- Quant triga el sistema en iniciar completament?

## Part 2 — Millores d’optimització

### 5. Desinstal·lació de paquets innecessaris
Llista els paquets més grans:
```
dpkg-query -Wf '${Installed-Size}	${Package}
' | sort -n | tail
```
Respon:
- Quins paquets ocupen més espai?
- Quin(s) podries eliminar sense afectar el sistema?

Ordre per eliminar un paquet:
```
sudo apt remove --purge <nom_paquet>
```

### 6. Optimització de l’arrencada
Desactiva un servei no necessari:
```
sudo systemctl disable nom_servei
```
Respon:
- Quin servei has desactivat?
- Per què no és necessari en la teva màquina?

### 7. Neteja de paquets i memòria
Executa:
```
sudo apt autoremove
sudo apt clean
```
Respon:
- Quants MB s’han alliberat?

### 8. Revisió de processos automàtics
Executa:
```
systemctl list-unit-files --type=service
```
Respon:
- Quin servei creus que consumeix recursos i podries desactivar?

## Part 3 — Millora del rendiment del disc

### 9. Analitza l’ús del disc per carpetes
Instal·la ncdu:
```
sudo apt install ncdu
sudo ncdu /
```
Respon:
- Quines carpetes ocupen més espai?
- És normal?

### 10. Activa TRIM (si tens SSD)
```
sudo systemctl enable fstrim.timer
sudo systemctl start fstrim.timer
```
Respon:
- Quin benefici té activar TRIM?

## Part 4 — Pregunta de reflexió
Quins tres passos d’optimització tindrien més impacte en un sistema Ubuntu amb pocs recursos (CPU, RAM i disc)? Justifica la resposta.
