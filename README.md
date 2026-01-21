# Gamemax Iceberg 240 - Linux Display Driver 🐧❄️

Este projeto é um driver em Python desenvolvido para controlar o display LCD do Water Cooler **Gamemax Iceberg 240** no Linux. Ele permite monitorar e exibir em tempo real a temperatura da CPU, o uso de processamento (%) e a rotação das ventoinhas (RPM).

**Desenvolvido por:** [CarlosDev](https://github.com/CarlosDev)

---

## 🚀 Funcionalidades
- **Monitoramento de CPU:** Uso percentual dinâmico.
- **Temperatura:** Leitura de sensores térmicos (Intel/AMD).
- **Fan RPM:** Captura específica do FAN 2 (via sensores da placa-mãe).
- **Compatibilidade:** Testado e funcional em **Python 3.14+** e **Fedora 43**.

---

## 🛠️ Pré-requisitos

Testado no **Fedora 43**. Se você utiliza outra distribuição, instale os pacotes equivalentes:

### **Fedora / Nobara**
```bash
sudo dnf install python3-pip libusb1 lm_sensors -y
pip install psutil pyusb

Ubuntu / Debian / Mint
Bash

sudo apt update && sudo apt install python3-pip python3-usb libusb-1.0-0 lm-sensors -y
pip install psutil pyusb --break-system-packages

⚙️ Configuração Crítica de Hardware

Siga estes passos caso os valores de RPM ou Temperatura apareçam zerados ou o dispositivo não seja detectado:
1. Parâmetro do Kernel (Correção de conflito ACPI)

    Edite o arquivo do GRUB:
    Bash

    sudo nano /etc/default/grub

    Adicione acpi_enforce_resources=lax dentro das aspas da linha GRUB_CMDLINE_LINUX_DEFAULT.

    Atualize o GRUB:

        Ubuntu/Debian: sudo update-grub

        Fedora/Arch: sudo grub-mkconfig -o /boot/grub/grub.cfg

    Reinicie o computador.

2. Ativação dos Sensores

Execute o comando abaixo e aceite todas as opções (digite y) para detectar os chips da sua placa-mãe:
Bash

sudo sensors-detect --auto

3. Permissões USB (udev)

Para permitir que o script acesse o USB sem necessidade de ROOT constante:
Bash

echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="5131", ATTR{idProduct}=="2007", MODE="0666"' | sudo tee /etc/udev/rules.d/99-gamemax.rules
sudo udevadm control --reload-rules && sudo udevadm trigger

💻 Como Executar

Certifique-se de salvar o código do driver como cooler.py e execute:
Bash

python3 cooler.py
