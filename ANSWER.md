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

![](https://github.com/user-attachments/assets/879db387-16f1-4041-afc5-b6512ffa3b72)

![](https://github.com/user-attachments/assets/7582adee-b990-4532-9129-0f555936bc52)

![](https://github.com/user-attachments/assets/485a771c-3e41-4ac8-8768-a8f064028dbb)

![](https://github.com/user-attachments/assets/6aaaa9e3-f79e-44f8-a7ac-5530a5993a5c)

![](https://github.com/user-attachments/assets/39684e66-872f-4633-b76f-88a428c5f3d5)

![](https://github.com/user-attachments/assets/91fb0a4b-b2b2-427f-9f11-d1a800ad80e9)
