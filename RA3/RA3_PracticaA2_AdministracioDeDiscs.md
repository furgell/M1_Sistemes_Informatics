# M1 – Sistemes Informàtics  
## RA3 · Pràctica A2: Administració de Discs

---

## 🧩 Descripció de la pràctica

Aquesta pràctica consisteix en **crear, particionar i muntar discs** dins de màquines virtuals amb **GParted, Ubuntu Server i Windows 10**, així com configurar el **muntatge automàtic d’un dispositiu USB**.

---

## 🔹 1. Màquina virtual amb GParted

### 1.1 Fer espai a disc i crear particions

1. Obrir la màquina virtual **Isard** o similar.  
2. Afegir un **nou disc virtual** o alliberar espai per crear dues particions de **2.5 GB** cadascuna.  
3. Obrir GParted:
   ```bash
   sudo gparted
   ```
4. Seleccionar el disc (ex. `/dev/sdb`) i crear dues particions de **2.5 GB**.  
5. Aplicar els canvis.

---

### 1.2 Crear quatre particions noves amb diferents formats

| Nº | Sistema de fitxers | Comanda o acció |
|----|---------------------|-----------------|
| 1  | FAT32 | `Format to → fat32` |
| 2  | NTFS  | `Format to → ntfs`  |
| 3  | ext3  | `Format to → ext3`  |
| 4  | ext4  | `Format to → ext4`  |

Comprovar les particions:
```bash
sudo fdisk -l
```

---

## 🐧 2. Ubuntu Server 18.04 o superior

### 2.1 Afegir espai a disc (5 GB)
Afegir un nou disc virtual de **5 GB** a la màquina.  
Verificar:
```bash
lsblk
```

---

### 2.2 Particionar el disc amb `fdisk`

```bash
sudo fdisk /dev/sdb
```

Ordres dins de `fdisk`:
```
n        # nova partició
p        # primària
1        # número de partició
<Enter>  # sector inicial per defecte
+5G      # mida de la partició
w        # escriure i sortir
```

---

### 2.3 Comprovar la taula de particions

```bash
sudo fdisk -l /dev/sdb
```

Exemple de resultat:
```
sdb    8:16   0    5G  0 disk
└─sdb1 8:17   0    5G  0 part
```

---

### 2.4 Formatar la partició amb ext4

```bash
sudo mkfs.ext4 /dev/sdb1
sudo blkid /dev/sdb1
```

Apunta l’UUID obtingut (per usar-lo a `/etc/fstab`).

---

### 2.5 Crear carpeta i muntar la partició

```bash
sudo mkdir /mnt/dades
sudo mount /dev/sdb1 /mnt/dades
df -h
```

---

### 2.6 Muntatge permanent (fitxer `/etc/fstab`)

```bash
sudo nano /etc/fstab
```

Afegir aquesta línia (substituir l’UUID pel real):
```
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  /mnt/dades  ext4  defaults  0  2
```

Provar:
```bash
sudo umount /mnt/dades
sudo mount -a
```

---

## 🪟 3. Windows 10 o superior

### 3.1 Crear espai de 5 GB

1. Obrir **Administració de discs**.  
2. Reduir volum → **5 GB**.

---

### 3.2 Crear dues particions de 2.5 GB

1. Clicar amb el botó dret sobre l’espai no assignat.  
2. Crear una partició de **2.5 GB** i una segona igual.

---

### 3.3 Formatar en NTFS

1. **Formatejar → NTFS**.  
2. Assignar lletres (E: i F:).  
3. Comprovar que es poden obrir i utilitzar.

---

## 🧠 4. Tasca d’investigació: muntatge automàtic d’un pendrive

**Objectiu:** muntar automàticament `/dev/sdb1` a `/media/usb`.

### Opció 1 – Afegir al fitxer `/etc/fstab`
```bash
sudo mkdir /media/usb
sudo blkid /dev/sdb1
sudo nano /etc/fstab
```

Afegir la línia:
```
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  /media/usb  vfat  defaults,nofail  0  0
```

Comprovar:
```bash
sudo mount -a
```

---

### Opció 2 – Automount amb systemd o autofs

També es pot crear una unitat `.mount` amb **systemd** o configurar **autofs** per muntatge automàtic quan es connecti el dispositiu.

---

## 📊 Resultat final esperat

| Sistema Operatiu | Acció realitzada | Format | Muntatge |
|------------------|------------------|---------|----------|
| Ubuntu Server | 1 partició de 5 GB | ext4 | `/mnt/dades` (fstab) |
| Windows 10 | 2 particions de 2.5 GB | NTFS | E: i F: |
| USB automàtic | `/dev/sdb1` | vfat | `/media/usb` automàtic |

---

**Autor:** _[Nom de l’alumne]_  
**Data:** 15/12/2025  
**Centre:** _Institut / Cicle Formatiu – 2025_
