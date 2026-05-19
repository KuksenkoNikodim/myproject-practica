
# Практическая работа: Настройка сервера и среды разработки

## 📌 Цель работы
Настроить удалённый сервер, организовать совместную работу через SSH, установить Webmin и подготовить среду для разработки на Python/Django.

---

## 🛠 Выполненные задачи

### 1. Подключение к серверу
- **IP:** `89.208.174.76`
- **Порт:** `2233`
- **Общий пользователь:** `cxuser`
- **Личный пользователь:** `nikod`
- Использован SSH-ключ `edu_key_ossh.pem`

### 2. Настройка VS Code
Установлены расширения:
- Remote - SSH
- Remote Explorer
- Python + Pylance
- Docker
- GitLens
- Django
- Data Wrangler

### 3. SSH-конфигурация
Файл `~/.ssh/config`:
``ssh-config
# Общий профиль
Host project-server
    HostName 89.208.174.76
    User cxuser
    Port 2233
    IdentityFile ~/Downloads/edu_key_ossh.pem

# Личный профиль
Host personal-server
    HostName 89.208.174.76
    User nikod
    Port 2233
    IdentityFile ~/Downloads/edu_key_ossh.pem

 4. Создание проекта
bash
cd /home/cxuser/projects
mkdir myproject
cd myproject
python3 -m venv venv
source venv/bin/activate
pip install django pandas numpy requests
pip freeze > requirements.txt

5. Установка Webmin
wget https://github.com/webmin/webmin/releases/download/2.202/webmin_2.202_all.deb
sudo dpkg -i webmin_2.202_all.deb

6. SSH-туннель для Webmin
   ssh -L 8080:localhost:10000 cxuser@89.208.174.76 -p 2233 -N
   Доступ в браузере: https://localhost:8080

   ## ❌ Ошибки и их решение

| Ошибка | Решение |
|--------|---------|
| Permission denied (publickey) | Ключ добавлен в SSH-агент через `ssh-add` |
| VS Code не видит сервер | Установлен Remote-SSH, настроен `config` |
| ERR_CONNECTION_TIMED_OUT порт 10000 | Использован SSH-туннель |
| bind: Permission denied порт 10000 | Порт заменён на 8080 |
| 403 Access denied Webmin | Выполнено sudo systemctl restart webmin |
| Ошибка GPG при установке Webmin | Установка через dpkg -i напрямую |

👥 Состав команды
Имя	Логин	Роль
Общий технический	cxuser	Работа над проектом
Никодим	nikod	Личный профиль
Дарья	daria	Второй участник
Сергей       Третий участник

## 📄 Команды для быстрого доступа

| Действие | Команда |
|----------|---------|
| Подключение к общему профилю | ssh project-server |
| Подключение к личному профилю | ssh personal-server |
| Туннель для Webmin | ssh -L 8080:localhost:10000 cxuser@89.208.174.76 -p 2233 -N |
| Webmin в браузере | `https://localhost:8080` |
| Активация VENV | `source /home/cxuser/projects/myproject/venv/bin/activate` |
