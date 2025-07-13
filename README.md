# unzipctl

A simple CLI tool to import, extract, and organize archive files (RAR, ZIP, etc.) on Linux or TrueNAS SCALE systems.

---

## 🚀 Features

✅ Supports RAR (including RAR5), ZIP, 7z, TAR, GZ, BZ2, XZ  
✅ Automated extraction loop via Docker container  
✅ CLI wrapper for easy moving, cleaning, and importing of archives  
✅ Configurable via a simple configuration file  
✅ Perfect for TrueNAS SCALE or any Linux environment

---

## 🔧 Installation

### 1. Clone the repository

```bash
git clone https://github.com/youruser/unzipctl.git
cd unzipctl
```

### 2. Install the script

```bash
sudo cp unzipctl /usr/local/bin/
sudo chmod +x /usr/local/bin/unzipctl
```

TrueNAS SCALE protects the root filesystem.
System updates could overwrite custom binaries.
So they keep /usr mostly read-only.

#### ✅ How to solve it

##### Pick a dataset, or create it

```bash
sudo mkdir -p /mnt/apps/scripts
```

##### Copy the script there

```bash
sudo cp unzipctl /mnt/apps/scripts/
sudo chmod +x /mnt/apps/scripts/unzipctl
```

##### Add it to your PATH

So you can just type unzipctl anywhere:
Edit your shell profile, e.g. .bashrc:

```bash
echo 'export PATH=$PATH:/mnt/apps/scripts' >> ~/.bashrc
source ~/.bashrc
```
Now just type:
```bash
unzipctl help
```

### 3. Copy and edit the configuration file
Copy the example config:

```bash
sudo cp unzipctl.conf.example /etc/unzipctl.conf
```
Then edit `/etc/unzipctl.conf` to match your own paths:
```bash
IMPORT_DIR="/mnt/apps/unzip/import"
UNPACKED_DIR="/mnt/apps/unzip/unpacked"
```

## ⚙️ Usage

### Import files
Copy one or more files to the import directory:
```bash
unzipctl import /path/to/myarchive.rar
```

### Re-import all unpacked files into the import folder
```bash
unzipctl import_all
```

### Move an unpacked file

Move a single file:
```bash
unzipctl move myfile.mkv /mnt/tank/movs/newfolder/
```
Or move and rename it:
```bash
unzipctl move myfile.mkv /mnt/tank/movs/newfolder/ newname.mkv
```
### Cleanup

Delete all contents from the import and unpacked directories:
```bash
unzipctl cleanup
```

### Show help

Display usage instructions:
```bash
unzipctl help
```
---
## 🐳 Using unzipctl with Docker

The unzipctl CLI tool works perfectly together with a Docker container that handles the extraction logic.

### Docker container features

✅ Automatically extracts all archives you place into the import directory via unzipctl import
✅ Supports RAR (including RAR5) via RARLAB’s official unrar
✅ Supports ZIP, 7z, TAR, GZ, BZ2, XZ via 7-Zip
✅ Runs continuously in the background and monitors the import directory

---

### Example Docker setup

Use the image like this:
```bash
crss1337/my-unzip:latest
```

#### Volumes:
| Host Path                | Container Path |
| ------------------------ | -------------- |
| /mnt/apps/unzip/import   | /import        |
| /mnt/apps/unzip/unpacked | /unpacked      |

#### Environment:
```ini
SLEEP_TIME=60
```

---

## Workflow

- Import archives into the import folder:
```bash
unzipctl import /path/to/myarchive.rar
```
- The container automatically extracts the files.
- Move the unpacked files:
```bash
unzipctl move myfile.mkv /mnt/tank/movs/newfolder/
```
- Clean up:
```bash
unzipctl cleanup
```
---
## ℹ️ About RARLAB’s unrar

The Docker container includes the official RARLAB unrar binary, which supports modern RAR formats like RAR5. Its use is permitted for private purposes according to the license.

More info: https://www.rarlab.com/rar_add.htm
--- 
## 🛠️ Contribution

Pull requests and issues are welcome! If you’d like to add new features or report bugs, feel free to contribute.

## License

This project is licensed under the MIT License. See LICENSE for details.
