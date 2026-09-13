# Infrastructure

## Описание

В репозитории собран набор компонентов для первоначальной настройки сервера и установки необходимых инструментов для последующего развёртывания бекенда.

## Как использовать?

### Предисловие

Перед работой необходимо: 
- Установить зависимости Ansible:

```sh
cd ansible/
ansible-galaxy install -r requirements.yaml
```

- Настроить [переменные](ansible/inventory/group_vars/all.yaml) для плейбуков

Если первоначальная настройка уже была выполнена, то вместо флага `--ask-pass` в командах ниже необходимо:

1. Добавить ваш ключ в ssh-agent
```sh
eval "$(ssh-agent -s)"
ssh-add <pathToPrivateKey>
```

2. Использовать флаги
```sh
... -e "ansible_user=<yourUser>" -e "ansible_port=<sshPort>"  --private-key <pathToPrivateKey>
```

### 1. Первоначальная настройка

**Что делает?**
- Устанавливает пакеты и докер роль
- Настраивает ssh
- Создаёт юзеров
- Настраивает UFW

1. Проверить работоспособность плейбука

```sh
# из папки ansible
ansible-playbook playbooks/bootstrap.yaml --diff --check --ask-pass
```

2. Применить изменения

```sh
ansible-playbook playbooks/bootstrap.yaml --diff --ask-pass
```

### 2. Настройка рабочего окружения

**Что делает?**
- Создаёт сервисный аккаунт, из-под которого будет работать весь бек
- Устанавливает github runner роль
- Генерирует sops-age ключ

1. Применить плейбук

```sh
export PERSONAL_ACCESS_TOKEN=<Classic GitHub PAT with 'admin:org' permissions>
ansible-playbook playbooks/workspace.yaml --diff --ask-pass
```

2. Скопировать public sops-age ключ и вставить в `.sops.yaml` в репозиториях
