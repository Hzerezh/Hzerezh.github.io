# 🔑 Как создать SSH-ключи для GitHub и добавить их в аккаунт

## 📌 Шаг 1: Проверка существующих SSH-ключей
Перед созданием нового ключа стоит проверить, есть ли уже сгенерированные ключи на вашем компьютере:

### Linux/macOS
```sh
ls -al ~/.ssh
```

### Windows (PowerShell)
```powershell
if (!(Test-Path -Path "$env:USERPROFILE\.ssh")) { New-Item -ItemType Directory -Path "$env:USERPROFILE\.ssh" }
Get-ChildItem -Path $env:USERPROFILE\.ssh
```

Если в списке файлов есть `id_rsa.pub` или `id_ed25519.pub`, то SSH-ключ уже существует.

## 📌 Шаг 2: Создание нового SSH-ключа
Если SSH-ключа нет или вы хотите создать новый, выполните следующую команду:

### Linux/macOS/Git Bash (Windows)
```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Windows (если `ed25519` не поддерживается)
```powershell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Замените `your_email@example.com` на ваш e-mail, который используется в GitHub.

После выполнения команды система попросит указать путь сохранения ключа. Оставьте по умолчанию (`~/.ssh/id_ed25519` или `~/.ssh/id_rsa`) и нажмите `Enter`.

Затем вас попросят ввести пароль для защиты ключа. Можно оставить пустым или ввести сложный пароль.

## 📌 Шаг 3: Добавление SSH-ключа в агент

### Linux/macOS
```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Windows (PowerShell)
Сначала проверьте статус `ssh-agent`:
```powershell
Get-Service ssh-agent
```
Если `Status` — `Stopped` или `Disabled`, выполните:
```powershell
Set-Service -Name ssh-agent -StartupType Automatic
Start-Service ssh-agent
```
Затем добавьте ключ:
```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

Если используется RSA:
```powershell
ssh-add $env:USERPROFILE\.ssh\id_rsa
```

## 📌 Шаг 4: Копирование SSH-ключа

### Linux/macOS/Git Bash
```sh
cat ~/.ssh/id_ed25519.pub
```

### Windows (PowerShell)
```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub
```

Скопируйте полученный ключ.

## 📌 Шаг 5: Добавление SSH-ключа в GitHub
1. Перейдите в [настройки GitHub](https://github.com/settings/keys).
2. Нажмите **New SSH key**.
3. В поле **Title** введите название ключа (например, "Мой ПК").
4. В поле **Key** вставьте скопированный SSH-ключ.
5. Нажмите **Add SSH key**.
6. Подтвердите операцию, если потребуется.

## 📌 Шаг 6: Проверка соединения с GitHub
Проверьте, успешно ли настроен SSH-доступ:

```sh
ssh -T git@github.com
```

Если при первом подключении появится сообщение:

```sh
The authenticity of host 'github.com (140.82.112.4)' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Введите `yes` и нажмите `Enter`. После этого SSH сохранит отпечаток ключа GitHub в `known_hosts`, и вопрос больше не появится.

Если появляется ошибка `Host key verification failed`, выполните команду:

```sh
ssh-keygen -R github.com
```

Затем попробуйте подключиться снова:

```sh
ssh -T git@github.com
```

Если всё настроено правильно, вы увидите сообщение:

```sh
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

Теперь вы можете использовать SSH для работы с репозиториями GitHub! 🎉

