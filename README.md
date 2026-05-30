# Ansible Docker Stack

Автоматизация развёртывания Docker-стека (Flask + PostgreSQL + Nginx) с помощью Ansible.

## Технологии

- Ansible
- Docker
- Docker Compose
- Nginx
- Flask
- PostgreSQL

## Архитектура

Ansible управляет удалённым хостом (server2) и выполняет:

1. Установку Docker и Docker Compose
2. Настройку пользователей и групп
3. Копирование docker-compose.yml
4. Запуск контейнеров

## Быстрая проверка

```bash
ansible -m ping all -i inventory/production.yml
ansible-playbook -i inventory/production.yml playbooks/setup-docker-stack.yml
```

## Результат на server2

- Frontend: `http://185.75.189.29:8080`
- API health: `http://185.75.189.29:8081/health`
- API db-check: `http://185.75.189.29:8081/db-check`

## Структура репозитория

- README.md
- ARCHITECTURE.md
- SETUP.md
- TROUBLESHOOTING.md
- inventory/
    - production.yml
- playbooks/
    - setup-docker-stack.yml
- screenshots/
    - ansible-playbook-run.png
    - docker-ps-server2.png
    - api-health.png
    - api-db-check.png
