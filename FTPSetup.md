# 🚀 FTP Server Setup on NVIDIA Jetson (MacOS Client)

This repository documents how to quickly install and configure an FTP server on an NVIDIA Jetson device, and how to connect to it from a MacOS machine.

---

## 💻 Server Side: Set Up FTP Server on Jetson

### 1. Install `vsftpd` (Very Secure FTP Daemon)

```bash
sudo apt update
sudo apt install vsftpd
```

### 2. Configure `vsftpd`

Edit the configuration file:

```bash
sudo nano /etc/vsftpd.conf
```

Recommended changes:

```
local_enable=YES
write_enable=YES
chroot_local_user=YES
```

Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X`).

Restart the FTP service:

```bash
sudo systemctl restart vsftpd
sudo systemctl enable vsftpd
```

### 3. (Optional) Firewall Check

If needed, check iptables:

```bash
sudo iptables -L
```

If no firewall is active, FTP should work by default.

---

## 🍏 Client Side: Set Up FTP Client on MacOS

### 1. Install Homebrew (if missing)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Add Homebrew to your PATH:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Check brew is working:

```bash
brew --version
```

### 2. Install `ftp` Command

Install `inetutils` (includes ftp):

```bash
brew install inetutils
```

---

## 🔗 Connect from Mac to Jetson

Use the `ftp` command to connect:

```bash
ftp <Jetson_IP_Address>
```

Example:

```bash
ftp 192.168.1.100
```

Login using your Jetson username and password.

---

## 📂 Quick Test Upload

Inside the FTP session:

```bash
put testfile.txt
```

Or from the MacOS command line:

```bash
ftp -n <Jetson_IP_Address>
```

Then:

```
user <username> <password>
put testfile.txt
bye
```

---

## 🧹 Future Improvements

- Add SFTP for more secure transfers
- Create a dedicated FTP-only user
- Automate server startup scripts
- Set up folder permissions for image dumping (e.g., `/home/roboflow/ftp_uploads/`)

---

## 📘 License

This project is provided as-is under the MIT License.
