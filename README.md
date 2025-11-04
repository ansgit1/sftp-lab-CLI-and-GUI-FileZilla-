# sftp-lab-CLI-and-GUI-FileZilla-

# 🔐 SFTP Lab — Kali Linux ↔ Windows (CLI & GUI)


his lab shows how to securely transfer files using SFTP (over SSH) between Kali Linux and Windows systems.
You will set up OpenSSH, connect both machines, and test uploading and downloading files using both command-line and FileZilla GUI methods.


 🧰 Tools Used

- Kali Linux – SFTP client (CLI) & SSH server (GUI)
- Windows 10 – SFTP server (for CLI mode)
- Windows Server 2016 – FileZilla Client (for GUI mode)
- OpenSSH – provides SSH/SFTP services
- FileZilla Client – GUI SFTP tool
- VMware Workstation – bridged network setup between VMs


 ⚙️ SFTP CLI Lab — Kali (Client) ↔ Windows 10 (Server)

 🖥️ Windows 10 Setup (Server Side)
powershell

# Install and start OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Start-Service sshd
Set-Service sshd -StartupType Automatic

# Create test user
net user sftplabtest Passw0rd! /add

## Install and start OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
Start-Service sshd
Set-Service sshd -StartupType Automatic

# Create test user
net user sftplabtest Passw0rd! /add

# Verify SFTP subsystem line exists in SSH configuration
findstr "Subsystem" "C:\ProgramData\ssh\sshd_config"

# (Expected output includes)
# Subsystem   sftp   sftp-server.exe (if you ar seeing this the SSH server is up and runnig )

# and run Get-Service sshd to confirm it will show out put like below 

( Status   Name               DisplayName
------   ----               -----------
Running  sshd               OpenSSH SSH Server )

# Restart SSH service
Restart-Service sshd



🧪 Kali Linux (Client Side)

# Connect to Windows via SFTP
sftp sftplabtest@192.168.x.x

# Navigation to dir 

pwd          # show remote dir
lpwd         # show local dir
ls / lls     # list remote/local files
cd / lcd     # change remote/local dir

# Transfers
get remotefile.txt          # download from Windows
put localfile.txt           # upload to Windows
put -r foldername           # upload folder recursively
bye                         # exit session

✅ Result: Successful login, file transfers both ways, verified uploads on Windows.

🖥️ SFTP GUI Lab — Windows Server 2016 (Client) ↔ Kali (Server)
🧰 Kali Linux Setup (SFTP Server)

Copy code
# Enable and start SSH service
sudo systemctl enable --now ssh

# Check service status
sudo systemctl status ssh

# Find Kali IP
ip a

💻 Windows Server 2016 Setup (FileZilla Client)
Open FileZilla Client → File → Site Manager → New Site

Configure:

Protocol: SFTP - SSH File Transfer Protocol

Host: Kali IP (e.g., 192.168.x.x)

Port: 22

User: username

Password: (Kali password)

Click Connect and accept 

Test Upload (Windows → Kali) and Download (Kali → Windows).


✅ Result: GUI connection successful, files transferred securely, logs verified.

📘 Outcome

   SFTP working in both CLI and GUI modes
   Verified secure file transfer between Kali ↔ Windows
   Network communication confirmed via bridged mode
   Tools tested: OpenSSH, FileZilla, VMware

Please find the screenshots of the CLI lab and GUI transfer logs in this repository
