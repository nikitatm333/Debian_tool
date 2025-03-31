# Debian_tool
Настройка дистрибутива Debian для разработки встраемых систем

## Установим git, docker и компилятор
### git:
```
sudo apt update && sudo apt install git -y
```
### Добавление репозитория docker:
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
### Установка Docker:
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```





