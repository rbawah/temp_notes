## How to Enable WSL 2 on Windows 
Follow the steps below to enable the Windows Subsystem for Linux (WSL) feature on Windows.

Microsoft recommends WSL 2 unless you have a very specific reason to stick with WSL 1 (like instant access to Windows file performance), please go with WSL2.

### Prerequisites

- Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11
- Administrator privileges


### The full WSL2 setup so you get the latest, faster version of the Windows Subsystem for Linux.

**Step 1: Enable WSL & Virtual Machine Platform**

```powershell
# run this command first
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

# then this second
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
Then restart your computer.

Troubleshooting
- If you get virtualization errors, ensure virtualization is enabled in your BIOS/UEFI settings
- Restart your PC and enter BIOS
- If you have an Intel Processor, look for something like `Intel VT-X` and enable it.
- If you have an AMD processor, it will be `AMD-V`, enable it.

**Step 2: Set WSL 2 as Default**
- After reboot, open your terminal (**NOT as admin**) and run:
```powershell
wsl.exe --update
```
Then set **WSL2** as the default version.
```powershell
wsl --set-default-version 2
```

**Step 3: Install a Linux Distro**

Check what’s available:
```powershell
wsl --list --online
```

Install Ubuntu:
```powershell
wsl.exe --install Ubuntu-24.04
```

**Step 4: Launch and Configure**

After installation:
- Open the distro (e.g., Ubuntu) from the Start menu.
- Create a `username` and `password`.
- You now have a Linux terminal inside Windows 🚀

**Step 5: Update Your Distro (Recommended)**

Inside the Linux shell, run:
```bash
sudo apt update && sudo apt upgrade -y
```

### Key Things to Know
File System Navigation:

- `/mnt/c/` = Your Windows C: drive
- `/home/your-username/` = Your Linux home directory (recommended for Linux work)

### To navigate to your Linux home:
```bash
cd ~
# or
cd /home/your-username
```

### Install essential tools:
```bash
sudo apt install curl wget git build-essential
```

### Check WSL version (from Windows PowerShell):
```powershell
wsl --list --verbose
```


### if you already have WSL1, you can switch between WSL 1 and WSL 2 for any installed Linux distribution:
**Step 1: List Installed Distros**

Run in **PowerShell**:
```powershell
wsl --list --verbose
```
You’ll see something like:
```pgsql
  NAME      STATE           VERSION
* Ubuntu    Running         2
  Debian    Stopped         1
```

VERSION = 1 or 2 → shows if that distro is using **WSL 1** or **WSL 2**.

**Step 2: Convert a Distro to WSL 2**

If you want to switch **Ubuntu** to **WSL 2**:
```powershell
wsl --set-version Ubuntu 2
```
⚠️ Conversion may take a few minutes if the distro has lots of data.

To switch back to WSL 1:
```powershell
wsl --set-version Ubuntu 1
```
**Step 3: Make WSL 2 the Default for New Installs**

So any new distro you install will use WSL 2:
```powershell
wsl --set-default-version 2
```



<!-- ## If the above process will not work for you, use the steps below:

1. Open **PowerShell as Administrator**
- Press `Win + X` → select **Windows PowerShell (Admin)** or **Terminal (Admin)**.

2. Run the command:
```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
3. Restart your computer when prompted.

### After enabling WSL
If you’re using Windows 10 (2004+) or Windows 11, you can directly install WSL and a Linux distro with:
```powershell
wsl --install
```
This installs the latest **Ubuntu** by default. -->
