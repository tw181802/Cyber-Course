# How to Set Up Kali NetHunter on Android (using Pixel Pro 8) (Rootless)

Follow these steps to install and set up Kali NetHunter on your Android device, such as the Pixel 8 Pro.

## Prerequisites:
- Android device running **Android 15** or newer.
- Internet connection.
- USB Debugging enabled.
- Developer Options enabled.

## Steps:

### 1. Enable Developer Options:
- Go to **Settings** > **About phone**.
- Android Version 15

![IMG_1159](https://github.com/user-attachments/assets/246381ec-0441-49e8-b6ba-458f5db60082)


![settings](https://github.com/user-attachments/assets/c7f6c694-2039-4dea-a5f9-a64ee7c6244a)

![IMG_1161](https://github.com/user-attachments/assets/736ecd2f-0637-44f2-b31b-857da3cd77d7)

### 2. Install Termux:
- Download and install the **Termux** app from [F-Droid](https://f-droid.org/packages/com.termux/), as it provides the latest version.
- **Do not use outdated versions** from the Play Store.
- Open Termux once installed.

![IMG_1162](https://github.com/user-attachments/assets/7a3b02a6-4bc9-4ae7-8ba3-77465cdbcbb0)

![IMG_1163](https://github.com/user-attachments/assets/09424627-9ee4-4a35-a399-b7c5a6d5a5d6)

### 3. Select First Version

![IMG_1164](https://github.com/user-attachments/assets/9017e368-41b1-4dbb-b16e-4da62fbfb49a)

### 4. Allow App and Install

![IMG_1165](https://github.com/user-attachments/assets/73458edd-ccdb-49cb-8c78-9ba119cf601d)

### 5. Click more details and Enter Pin to install anyway

![IMG_1166](https://github.com/user-attachments/assets/d1776e6b-0519-4362-83ea-cf6ab3a2dafe)


### 6. Open it 

![IMG_1167](https://github.com/user-attachments/assets/5a61f640-d84e-4941-8242-8443ecf48095)

![IMG_1168](https://github.com/user-attachments/assets/a7806110-9b12-4ef7-ac34-d8ea7861dee4)


### 3. Update Termux Packages:
In the Termux terminal, run the following command to update the package list:
```pkg update -y```

![IMG_1169](https://github.com/user-attachments/assets/68c6496f-73ad-49df-8555-3a98d0a2cf4b)


## Steps to Install Kali NetHunter on Android (Rootless)

### 1. Set Up Storage
### Allow Termux to access your device storage by running:

```termux-setup-storage```

![IMG_1170](https://github.com/user-attachments/assets/5d75fe95-4813-445c-bf8f-124dadd3fbe1)
![IMG_1171](https://github.com/user-attachments/assets/99c56ae8-4e04-486f-aa93-5d47896b2867)


### 2. Install Dependencies and Kali NetHunter

### Install necessary packages:

```pkg install wget```

```wget -O install-nethunter-termux https://offs.ec/2MceZWr```

![IMG_1172](https://github.com/user-attachments/assets/85b29dae-f01f-4e85-a44a-ad087df45619)



### 3. Change Permissions to Allow Execution
### Make the script executable:

`chmod +x installer-nethunter-termux`
![IMG_1174](https://github.com/user-attachments/assets/37fecd9a-c2a1-4144-b551-a5c411c84326)


### 4. Install NetHunter Rootless Install
### Run the installer script:

`./nethunter-installer-termux`
![IMG_1175](https://github.com/user-attachments/assets/465f298b-87d0-467e-812e-ae92ed18460e)


### When prompted, select Option 1 to install the full version of NetHunter.
### The installation may take some time and might require running the script twice to complete.
![IMG_1176](https://github.com/user-attachments/assets/25ad7b27-8ba7-4aae-bb75-4b7de4e121ce)



### 5. Choose Installation Options
### When asked whether to delete the root filesystem, press N to keep it.
![IMG_1178](https://github.com/user-attachments/assets/c3e18d88-ef42-4fbe-8659-a314fab1d5f4)

### Commands
- To start the CLI `nethunter`
- To setup the netHunter kex password `nethunter kex passwd`
- To start NetHunter KeX (Password will be set on first startup) `nethunter kex`
- To stop the NetHunter KeX GUI `nethunter kex stop` 
- To run NetHunter as root `nethunter -r`
- You replace nethunter with nh in all these commands. `nh`


### 6. Configure the Kali NetHunter GUI
### To start the Kali NetHunter GUI, Download from Link Below
```https://store.nethunter.com/packages/com.offsec.nethunter.store/```

![IMG_1181](https://github.com/user-attachments/assets/717a2cd3-54a0-4104-aeb2-12978f8efe99)

![IMG_1183](https://github.com/user-attachments/assets/5b178f66-069f-47c7-b84a-bdec28cdfd4d)

![IMG_1182](https://github.com/user-attachments/assets/56235198-7bfe-43fe-8997-f7bae2b3f0fc)

`nethunter kex &`
### 7. Troubleshooting
### If you encounter issues, such as problems with child process restrictions, you may need to disable certain security features or tweak your Termux configuration.

### Afterwards 
### Go to settings.
### Scroll down to About phone and press on it.
### Press on Software information.
### Tap Build number 7 times to enable developer mode.
### Press back twice. 
### Press on Developer options.(stop kali gui from being torn down) make note of port number 
### Enable USB debugging

![IMG_1161](https://github.com/user-attachments/assets/64349fb6-9861-4e18-a5aa-4933ee8c2449)

