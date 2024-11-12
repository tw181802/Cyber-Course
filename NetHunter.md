# How to Set Up Kali NetHunter on Android (Rootless)

Follow these steps to install and set up Kali NetHunter on your Android device, such as the Pixel 8 Pro.

## Prerequisites:
- Android device running **Android 15** or newer.
- Internet connection.
- USB Debugging enabled.
- Developer Options enabled.

## Steps:

### 1. Enable Developer Options:
- Go to **Settings** > **About phone**.
- Tap on **Build number** 7 times to enable **Developer options**.
- Go back to **Settings** > **Developer options**.
- Enable **USB debugging**.

### 2. Install Termux:
- Download and install the **Termux** app from [F-Droid](https://f-droid.org/packages/com.termux/), as it provides the latest version.
- **Do not use outdated versions** from the Play Store.
- Open Termux once installed.

### 3. Update Termux Packages:
In the Termux terminal, run the following command to update the package list:
```bash
pkg update && pkg upgrade

## Steps to Install Kali NetHunter on Android (Rootless)

### 4. Set Up Storage
Allow Termux to access your device storage by running:

```bash
termux-setup-storage


5. Install Dependencies
Install necessary packages:

pkg install wget
6. Install Kali NetHunter
Change directory to where the script will be downloaded:

cd ~
Download and install NetHunter by running:

wget https://github.com/OffensiveSecurity/kali-nethunter/releases/download/2023.1/kali-nethunter-arm64-2023.1.zip
After downloading, unzip the file:

unzip kali-nethunter-arm64-2023.1.zip
7. Change Permissions to Allow Execution
Make the script executable:

chmod +x nethunter-installer.sh
8. Install NetHunter
Run the installer script:

./nethunter-installer.sh
When prompted, select Option 1 to install the full version of NetHunter.
The installation may take some time and might require running the script twice to complete.

9. Choose Installation Options
When asked whether to delete the root filesystem, press N to keep it.

10. Configure the Kali NetHunter GUI
To start the Kali NetHunter GUI, use the following command in Termux:

nethunter kex &
11. Troubleshooting
If you encounter issues, such as problems with child process restrictions, you may need to disable certain security features or tweak your Termux configuration.

