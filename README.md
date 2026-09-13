# Infrastructure

## Описание

В репозитории собран набор компонентов для первоначальной настройки сервера и установки необходимых инструментов для последующего развёртывания бекенда.

## Как использовать?

### 1. Первоначальная настройка

1. Проверить работоспособность плейбука

```sh
cd ansible
ansible-playbook playbooks/bootstrap.yaml --ask-pass --check --diff
```

2. Примените изменения

```sh
ansible-playbook playbooks/bootstrap.yaml --ask-pass
```
