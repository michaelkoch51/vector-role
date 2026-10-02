# vector-role

Роль Ansible для установки и настройки [Vector](https://vector.dev/).

## Особенности

Архив Vector копируется с control-node (машины, где запускается Ansible)
через SSH. Это позволяет разворачивать Vector на хостах без внешнего
интернета — важно, если у ВМ нет исходящего доступа (например, из-за
проблем с NAT в Yandex Cloud).

## Переменные

| Переменная          | По умолчанию                                                | Описание                      |
|---------------------|-------------------------------------------------------------|-------------------------------|
| vector_version      | 0.34.1                                                      | Версия Vector                 |
| vector_bin          | /usr/local/bin/vector                                       | Путь к бинарю                 |
| vector_user         | vector                                                      | Пользователь сервиса          |
| vector_group        | vector                                                      | Группа сервиса                |
| vector_data_dir     | /var/lib/vector                                             | Каталог данных                |
| vector_config_dir   | /etc/vector                                                 | Каталог конфигурации          |
| vector_archive_name | vector-{{ vector_version }}-x86_64-unknown-linux-gnu.tar.gz | Имя архива                    |
| vector_archive_src  | files/{{ vector_archive_name }}                             | Путь к архиву на control-node |

## Требования

Файл `files/vector-<version>-x86_64-unknown-linux-gnu.tar.gz` должен
находиться рядом с playbook.

## Пример

    - hosts: vector
      become: true
      roles:
        - vector-role
