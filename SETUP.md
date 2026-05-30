# Установка и настройка

## Требования

- Управляющий узел (server1) с Ubuntu и Ansible
- Управляемый узел (server2) с Ubuntu и SSH-доступом
- Настроен passwordless sudo на server2

## Установка Ansible на server1

```bash
sudo apt update
sudo apt install ansible -y
```

## Настройка SSH-доступа

```bash
ssh-copy-id user@185.75.189.29
```

## Настройка passwordless sudo на server2

Подключитесь к server2:

```bash
ssh user@185.75.189.29
```

Выполните:

```bash
echo "user ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/user
```

## Запуск плейбука

На server1:

```bash
cd ~/ansible-docker-stack
ansible-playbook -i inventory/production.yml playbooks/setup-docker-stack.yml
```

## Проверка

На server2:

```bash
cd ~/docker-env
docker-compose ps
curl http://localhost:8081/health
```

