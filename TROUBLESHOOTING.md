# Поиск и устранение неисправностей

## 1. Ошибка: Missing sudo password

**Симптом:** Плейбук падает с ошибкой `Missing sudo password`.

**Причина:** На managed node не настроен passwordless sudo.

**Решение:** На server2 выполнить:

```bash
echo "user ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/user
```

## 2. Ошибка: build path /home/user/docker-env/backend does not exist

**Симптом:** Ошибка при выполнении `docker-compose up`.

**Причина:** Не скопированы исходные файлы приложения (backend, frontend).

**Решение:** Скопировать вручную с server1 на server2:

```bash
scp -r ~/docker-environment/* user@185.75.189.29:/home/user/docker-env/
```

## 3. Docker контейнеры не запускаются

**Проверка на server2:**

```bash
cd ~/docker-env
docker-compose logs
```

**Решение:** Перезапустить контейнеры:

```bash
docker-compose down
docker-compose up -d
```

## 4. API не отвечает

**Проверка:**

```bash
curl http://localhost:8081/health
curl http://localhost:8081/db-check
docker-compose ps
```

**Решение:** Проверить логи backend:

```bash
docker-compose logs backend
```

## 5. Не удаётся подключиться по SSH

**Проверка на server2:** Убедитесь, что в файле `/etc/ssh/sshd_config`:

```
PasswordAuthentication no
PermitRootLogin no
```

**Решение:** Перезапустите SSH:

```bash
sudo systemctl restart sshd
```

## 6. Ansible не видит server2

**Проверка:**

```bash
ansible -m ping all -i inventory/production.yml
```

**Решение:** Проверить инвентарь:

```bash
cat inventory/production.yml
```

Должно быть:

```yaml
all:
  hosts:
    server2:
      ansible_host: 185.75.189.29
      ansible_user: user
```

## 7. Ошибка: Permission denied (publickey)

**Причина:** SSH-ключ не скопирован на server2.

**Решение:** Скопировать ключ:

```bash
ssh-copy-id user@185.75.189.29
```
