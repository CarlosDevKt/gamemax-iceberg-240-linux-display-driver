# ❄️ Gamemax Iceberg 240 – Linux Display Driver 🐧

This project is a **Python-based driver** developed to control the LCD display of the  
**Gamemax Iceberg 240** water cooler on Linux.

It allows real-time monitoring and display of:

- 🌡️ CPU temperature  
- 📊 CPU usage (%)  
- 🌀 Fan rotation speed (RPM)

---

## 🚀 Features

- Real-time CPU monitoring  
- Temperature reading (Intel / AMD)  
- FAN 2 RPM reading  
- Compatible with **Python 3.14+**  
- Tested on **Fedora 43**

---

## 🛠️ Requirements

### 🟦 Fedora / Nobara
~~~bash
sudo dnf install python3-pip libusb1 lm_sensors -y
pip install psutil pyusb
~~~

### 🟧 Ubuntu / Debian / Mint
~~~bash
sudo apt update && sudo apt install python3-pip python3-usb libusb-1.0-0 lm-sensors -y
pip install psutil pyusb --break-system-packages
~~~

---

## ⚙️ Critical Hardware Configuration

⚠️ Follow **section 1️⃣ only if**:
- RPM shows as `0`
- Temperature shows as `0`
- The USB device is not detected

---

### 1️⃣ ACPI Conflict Fix (Kernel)

Edit the GRUB configuration:
~~~bash
sudo nano /etc/default/grub
~~~

Add the following inside `GRUB_CMDLINE_LINUX_DEFAULT`:
~~~text
acpi_enforce_resources=lax
~~~

Update GRUB:

**Ubuntu / Debian**
~~~bash
sudo update-grub
~~~

**Fedora / Arch**
~~~bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
~~~

➡️ Reboot the system.

---

### 2️⃣ Sensor Activation
~~~bash
sudo sensors-detect --auto
~~~

---

### 3️⃣ USB Permissions (udev)
~~~bash
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="5131", ATTR{idProduct}=="2007", MODE="0666"' | sudo tee /etc/udev/rules.d/99-gamemax.rules
sudo udevadm control --reload-rules && sudo udevadm trigger
~~~

---

## 💻 How to Run
~~~bash
python cooler.py
~~~

---

## 📌 Notes

- Check if the device appears in `lsusb`
- No need to run as root after configuring udev
- Secure Boot may block sensor modules
- If you want to run the script at startup using systemd, follow this tutorial:  
  https://www.codementor.io/@ufuksfk/how-to-run-a-python-script-in-linux-with-systemd-1nh2x3hi0e
---
