# Debian_tool
Настройка дистрибутива Debian для разработки встраемых систем

Установим git, docker и компилятор
git:
```
sudo apt update && sudo apt install git -y
```
Добавление репозитория docker:
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
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc]
https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt update
```
