## 🐳 Переустановка Docker и Docker Compose на Ubuntu

**Что делаем:**
Удаляем старую установку `docker` и `docker-compose`, затем ставим последнюю версию Docker CE + Compose plugin. Добавляем пользователя в группу `docker`.

---

### 🔥 Удаление старой версии

```bash
sudo apt purge docker docker-compose -y
sudo apt autoremove
```

### 📦 Установка Docker CE + Compose Plugin

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] \
https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 👤 Добавление пользователя в группу `docker`

```bash
sudo usermod -aG docker $USER
newgrp docker
```

✅ Теперь можно использовать современный синтаксис
```
docker compose up
```
