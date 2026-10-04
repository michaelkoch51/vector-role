# Домашнее задание к занятию 5 «Тестирование roles»

## Репозиторий

https://github.com/michaelkoch51/vector-role

## Molecule

Сценарий создан в `molecule/default/`. Тестируются два дистрибутива:
`ubuntu:latest` и `oraclelinux:8`.

Проверки в `molecule/default/verify.yml`:
- бинарь `/usr/local/bin/vector` существует и исполняем,
- конфиг `/etc/vector/vector.toml` существует,
- конфиг содержит секции `[sources.in]` и `[sinks.out]`.

`molecule test` выполняется полностью, включая шаг `idempotence`
(повторный прогон — `changed=0`), что подтверждает идемпотентность роли.

Особенности:
- Задачи, связанные с systemd (`Deploy vector systemd unit`,
  `Enable and start vector`), помечены тегом `molecule-notest` —
  в тестовом окружении (Docker-контейнеры без systemd) они пропускаются.
- Роль работает на обоих семействах ОС — Ubuntu и Oracle Linux.

**Тег:** `v1.1.0`

## Tox

Создан `tox.ini` и облегчённый сценарий `molecule/podman/`
с драйвером podman.

Запуск `tox` внутри контейнера `aragast/netology` невозможен
из-за ограничений Podman-in-Docker на Apple Silicon (ARM64 + Rosetta):
- `crun` не работает через Rosetta (ошибка memfd),
- `runc` не поддерживает режим `NoCgroups`.

Это инфраструктурное ограничение, не связанное с ролью.
Скриншоты попытки запуска приложены.

**Тег:** `v1.2.0`

## Скриншоты

См. папку `screenshots/` (или приложены отдельно к сдаче).
