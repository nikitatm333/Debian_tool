# Debian_tool
Настройка дистрибутива Debian для разработки встраемых систем

# Установим git, docker 
## git:
```
sudo apt update && sudo apt install git -y
```
## Добавление репозитория Docker:
```
sudo apt update
```
```
sudo apt install ca-certificates curl gnupg -y
```
```
sudo install -m 0755 -d /etc/apt/keyrings
```
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
```
```
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian bookworm stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt update
```
## Установка Docker:
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
### Чтобы запускать Docker без sudo, добавьте себя в группу docker:
```
sudo usermod -aG docker $USER
```

# Необходимые зависимости для начала работы
## Обновление системы
```
sudo apt update
```
```
sudo apt upgrade
```

## Установка необходимых инструментов
```
sudo apt install -y build-essential make libtool pkg-config cmake curl automake autoconf gcc git texinfo python3-dev libpython3-dev liblzma5 libncurses5 libncurses5-dev libusb-1.0-0-dev libgtk-3-dev libstlink-dev libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev xz-utils tk-dev
```

# Набор инструментов: компилятор, линковщик, ассемблер, отладчик и т.п.

Набор инструментов включает в себя:
- Компилятор;
- Компоновщик;
- Библиотеки времени выполнения.

## Получаем значение последней версии тулчейна:

```
ARM_TOOLCHAIN_VERSION=$(curl -s https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads | grep -Po '<h4>Version \K.+(?=</h4>)')
```
## Далее скачиваем сам тулчейн:
```
curl -Lo gcc-arm-none-eabi.tar.xz "https://developer.arm.com/-/media/Files/downloads/gnu/${ARM_TOOLCHAIN_VERSION}/binrel/arm-gnu-toolchain-${ARM_TOOLCHAIN_VERSION}-x86_64-arm-none-eabi.tar.xz"
```
### Если загрузка ломается, то можно попробовать сменить DNS сервер, например:
```
sudo nano /etc/resolv.conf
```
```
nameserver 8.8.8.8
```
## Создаем директорию, где будет находиться тулчейн:
```
sudo mkdir /opt/gcc-arm-none-eabi
```
## Извлекаем архив в эту директорию:
```
sudo tar xf gcc-arm-none-eabi.tar.xz --strip-components=1 -C /opt/gcc-arm-none-eabi
```

## Добавляем эту директорию в PATH-переменную:
```
echo 'export PATH=$PATH:/opt/gcc-arm-none-eabi/bin' | sudo tee -a /home/USER_NAME/.bashrc
```

# Утилиты для работы с ST-Link
```
mkdir ~/sources && cd ~/sources
sudo apt install libstlink-dev
git clone https://github.com/stlink-org/stlink.git
cd stlink
make clean
make release
sudo make install
```

## Далее необходимо установить права доступа к реальному оборудованию через установку правил udev:
```
sudo cp -a config/udev/rules.d/* /lib/udev/rules.d/
sudo udevadm control --reload-rules && sudo udevadm trigger
```

# Установка STM32CubeIDE
## Скачиваем программное обеспечение https://www.st.com/en/development-tools/stm32cubeide.html 
### Рекомендую скачивать STM32CubeIDE Generic Linux Installer, а не STM32CubeIDE Debian Linux Installer
```
cd ~/Downloads
```
## Даем права на исполнение:
```
chmod +x st-stm32cubeide_1.18.0_24413_20250227_1633_amd64.sh
```
## Выполняем установку:
```
sudo ./st-stm32cubeide_1.18.0_24413_20250227_1633_amd64.sh
```
## Запускаем IDE:
```
/opt/st/stm32cubeide_1.18.0/STM32CubeIDE
```

# Установка репозитория:
## Создаем STM32Cube и Repository
```
mkdir -p /home/USER_NAME/STM32Cube/Repository
```

## Устанавливаем репозиторий под Вашу серию МК https://cloud.mail.ru/public/2i19/Y4w8kKEiZ в Repository









