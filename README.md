# Debian_tool
Настройка дистрибутива Debian для разработки встраемых систем

# Установим git, docker и компилятор
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

## Необходимые зависимости для начала работы
## Добавление репозиториев и ключей
```
sudo wget -qO /etc/apt/trusted.gpg.d/kitware-key.asc https://apt.kitware.com/keys/kitware-archive-latest.asc
```
- Загружает GPG-ключ для репозитория Kitware (используется для установки CMake).
```
echo "deb https://apt.kitware.com/ubuntu/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/kitware.list
```
- Добавляет новый источник пакетов (репозиторий Kitware) в список sources.list.d.
- $(lsb_release -sc) — автоматически подставляет версию дистрибутива (например, bookworm для Debian 12).
```
sudo add-apt-repository -y ppa:git-core/ppa
```
- Подключает PPA-репозиторий с последними версиями git.

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




