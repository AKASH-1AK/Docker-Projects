# 📌 Project: Secure SSH Communication in WSL Ubuntu

This project demonstrates setting up an **OpenSSH server and client** within **WSL Ubuntu** to enable secure remote access and communication between multiple containers or virtual environments.

## 📜 Overview

- **Server:** Runs OpenSSH server (`openssh-server`) to allow secure remote connections.
- **Client:** Runs OpenSSH client (`openssh-client`) to connect to the server.
- **Authentication:** Uses SSH keys for secure access.
- **Benefits:** Improved security, better collaboration, scalability, portability, and ease of management.

---

## 🚀 Installation & Setup Guide

### **Step 1: Update and Install OpenSSH in WSL Ubuntu**
Before setting up SSH, ensure your system is up-to-date.

```bash
sudo apt update && sudo apt upgrade -y
```

Then, install OpenSSH server and client:

```bash
sudo apt install openssh-server openssh-client -y
```

### **Step 2: Start and Enable the SSH Service**
Once installed, start the OpenSSH server:

```bash
sudo service ssh start
```

Enable it to start automatically on boot:

```bash
sudo systemctl enable ssh
```

Check the status of the SSH service:

```bash
sudo systemctl status ssh
```

If the service is running, you should see output like:

```
● ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
   Active: active (running)
```

### **Step 3: Configure SSH for Secure Access**
Modify the SSH configuration file to allow remote connections:

```bash
sudo nano /etc/ssh/sshd_config
```

Find the following lines and update them:

```ini
PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes
```

Save the file (`Ctrl + X`, then `Y`, then `Enter`).

Restart the SSH service for the changes to take effect:

```bash
sudo systemctl restart ssh
```

### **Step 4: Generate SSH Keys for Authentication**
On the **client machine**, generate an SSH key pair:

```bash
ssh-keygen -t rsa -b 4096
```

This creates a public/private key pair stored in `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`.

Copy the public key to the server:

```bash
ssh-copy-id username@server-ip
```

If `ssh-copy-id` is not available, manually copy the public key:

```bash
cat ~/.ssh/id_rsa.pub | ssh username@server-ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Set correct permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### **Step 5: Connect to the SSH Server**
Now, you can securely connect to the server from the client:

```bash
ssh username@server-ip
```

Replace `username` with your actual Ubuntu username and `server-ip` with the server's IP address.

---

## 🔧 Troubleshooting

1. **Check if SSH is running**
   ```bash
   sudo systemctl status ssh
   ```
2. **Restart the SSH service**
   ```bash
   sudo systemctl restart ssh
   ```
3. **Check firewall rules (if applicable)**
   ```bash
   sudo ufw allow ssh
   sudo ufw enable
   ```

---

## 📌 Features & Benefits

✅ Improved security  
✅ Ease of management  
✅ Better collaboration  
✅ Scalability  
✅ Portability  

---

## 📂 Project Structure

```
/project1
│── setup_ssh.sh       # Script for automatic installation & setup
│── README.md          # Detailed documentation
