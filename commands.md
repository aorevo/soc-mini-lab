# Использованные команды

## Проверка SSH-сервиса

```bash
sudo systemctl status ssh
```

Команда использовалась для проверки состояния SSH-сервиса.

## Проверка открытого SSH-порта

```bash
sudo ss -tulpen | grep :22
```

Команда использовалась для проверки, что SSH-сервис слушает порт 22.

## Просмотр SSH-событий за текущий день

```bash
sudo journalctl -u ssh --since "today"
```

Команда использовалась для просмотра журналов SSH-сервиса за текущий день.

## Поиск подозрительных SSH-событий

```bash
sudo journalctl -u ssh --since "today" | grep -Ei "invalid user|connection closed|preauth"
```

Команда использовалась для поиска событий, связанных с попытками входа под несуществующим пользователем и закрытием соединений на этапе предварительной аутентификации.

## Сохранение найденных событий в файл

```bash
sudo journalctl -u ssh --since "today" | grep -Ei "invalid user|connection closed|preauth" > raw-ssh-events.log
```

Команда использовалась для сохранения найденных SSH-событий в отдельный файл.

## Очистка логов от личных данных

```bash
sed -i -E 's/ubuntu/LAB_HOST/g; s/vboxuser/LAB_USER/g; s/labuser/LAB_USER/g; s/fakeuser/INVALID_USER/g; s/::1/LOCALHOST_IPV6/g' sample-logs/auth-ssh-sample.log
```

Команда использовалась для замены имени хоста, пользователей и локального IP-адреса на обезличенные значения.