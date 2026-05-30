# Архитектура проекта

## Схема работы

- Control node (server1) → Managed node (server2)
- Ansible подключается по SSH
- Выполняет плейбук с задачами
- Результат: запущенные Docker-контейнеры

## Компоненты

| Компонент | Роль |
|-----------|------|
| inventory/production.yml | Список управляемых хостов |
| playbooks/setup-docker-stack.yml | Плейбук с задачами |
| docker-compose.yml | Описание контейнеров (копируется на server2) |

## Задачи плейбука

1. Update apt cache
2. Install Docker и Docker Compose
3. Start и enable Docker service
4. Add user to docker group
5. Create directory for docker-compose
6. Copy docker-compose.yml to remote host
7. Run docker-compose up

## Управляемый хост

- IP: 185.75.189.29
- Пользователь: user
- Доступ: по SSH-ключу
- Sudo: без пароля (NOPASSWD)
