# Official Telegram MTProto Proxy (Docker Compose)

Репозиторий содержит конфигурацию для развертывания официального прокси-сервера Telegram на базе Docker Compose. Конфигурация использует порт **4433**, оставляя стандартный порт **443** свободным для других сервисов.

## 🛠 Подготовка системы

### 1. Генерация секретного ключа (Secret)
Сгенерируйте 32-символьный шестнадцатеричный ключ командой:
```bash
openssl rand -hex 16
```

### 2. Установка Docker и Compose

#### Ubuntu / Debian:

```bash
sudo apt update && sudo apt install -y docker.io docker-compose-v2
sudo systemctl enable --now docker
```

#### CentOS / RHEL:
```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-compose-v2
sudo systemctl enable --now docker
```

## 🚀 Установка и запуск

1. Клонируйте репозиторий:
```bash
git clone https://github.com/Ilsolang/MTProto-Proxy-Server.git
cd MTProto-Proxy-Server
```
2. Настройте конфигурацию:

    - Откройте файл docker-compose.yml.
    - Замените YOUR_SECRET_HERE на ключ, сгенерированный ранее.

3. Запустите сервис:
```bash
docker compose up -d
```

## 🛡 Настройка Firewall

### Разрешите входящий трафик на порт 4433:

#### UFW (Ubuntu / Debian):
```bash
sudo ufw allow 4433/tcp
sudo ufw reload
```

#### Firewalld (CentOS / RHEL):
```bash
sudo firewall-cmd --permanent --add-port=4433/tcp
sudo firewall-cmd --reload
```

## 🔗 Подключение

#### Ссылка для добавления прокси в Telegram:
```bash
tg://proxy?server=ВАШ_IP&port=4433&secret=ВАШ_СЕКРЕТ
```

## 📝 Особенности

- Используется официальный образ telegrammessenger/proxy.
- Порт 4433 проброшен на внутренний порт 443 контейнера.
- Образ поддерживает только классический MTProto (без FakeTLS/ee-секретов).





