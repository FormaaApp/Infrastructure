# Infrastructure

## Описание

В репозитории собран набор компонентов для первоначальной настройки сервера и установки необходимых инструментов для последующего развёртывания бекенда.

## Как использовать?

### Предисловие

Перед работой необходимо установить зависимости Ansible:

```sh
cd ansible
ansible-galaxy install -r requirements.yaml
```

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

```sh
export PERSONAL_ACCESS_TOKEN=<Classic GitHub PAT with 'admin:org' permissions>
ansible-playbook playbooks/workspace.yaml --diff --ask-pass
```
