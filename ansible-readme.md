
# Ansible-деплой веб-приложения (CGI + Apache)

## Описание

Данный ansible-проект предназначен для автоматической установки и настройки веб-приложения (CGI-скрипт на Python) под Apache на Ubuntu.  
В результате развёртывания сайт будет доступен по адресу http://localhost/, поддерживается конвертация изображений JPG/PNG в чёрно-белое.

---

## Состав проекта

- **ansible/ansible.cfg** — базовая конфигурация ansible
- **ansible/inventory.yml** — инвентори с описанием хостов (здесь только localhost)
- **ansible/deploy.yml** — основной playbook для деплоя
- **ansible/files/** — папка с файлами проекта (CGI-скрипт, html-форма, apache-конфиг)

---

## Требования

- Ubuntu 22.04/24.04
- Установленный ansible  
  (если не установлен:  
  `sudo apt update && sudo apt install ansible -y`)

---

## Запуск

1. Перейти в папку ansible проекта:
    ```bash
    cd /home/lyalkid/code/ansible
    ```
2. Запустить playbook:
    ```bash
    ansible-playbook deploy.yml
    ```
3. Дождаться окончания работы ansible без ошибок.

---

## После деплоя

- Открой браузер и перейди по адресу:
  ```
  http://localhost/
  ```
- Загрузить jpg/png файл и проверить результат.
- Все файлы хранятся в /var/www/webapp/

---

## Полезные команды

- **Включить mod_cgid (если надо вручную):**
    ```bash
    sudo a2enmod cgid
    sudo systemctl restart apache2
    ```
- **Проверить статус apache:**
    ```bash
    sudo systemctl status apache2
    ```
- **Смотреть логи ошибок:**
    ```bash
    sudo tail -n 50 /var/log/apache2/error.log
    ```

---

## Примечания

- Проект не требует запуска python-скриптов вручную — всё работает через Apache и CGI.
- При необходимости внесения изменений в CGI-скрипт или HTML — обновите соответствующие файлы в папке `ansible/files/` и повторно запустите playbook.

---

**Вопросы, баги или предложения — смело пиши!**
