# Серверний push (експериментальна функція)

Серверний push - це функція надсилання повідомлень безпосередньо на мобільний телефон після завершення завантаження торента. Для цього не потрібно, щоб мобільний додаток постійно оновлював список торентів у фоновому режимі, достатньо налаштувати "Запускати зовнішню програму після завершення завантаження торента" на вашому сервері qBittorrent.

**Примітка**:
Серверний Push наразі є експериментальною функцією, і немає гарантії, що вона працюватиме повноцінно, особливо якщо ви перебуваєте в регіоні, де Google не має безперебійного доступу.

## Як використовувати

Необхідні умови:

1. Ви можете безперешкодно отримати доступ до Google у вашому регіоні (оскільки використовується служба push-сповіщень, що надається Firebase)
2. У середовищі виконання вашого сервера qBittorrent є програми, які можуть отримати доступ до мережі, наприклад curl. Якщо у вашій системі його немає, рекомендується встановити [curl](https://curl.se/). У наступних кроках як приклад буде використовуватися curl

Якщо ви впевнені, що наведені вище умови виконано, продовжуйте наступні кроки:

1. Створіть користувача в додатку
2. Скопіюйте створеного користувача, відкрийте веб-інтерфейс qBittorrent, натисніть "Налаштування" -> "Завантаження" та введіть `curl --form-string "message=%N завантаження завершено" "https://qbpush.fengmlo.com/api/v1/push/ваш-користувач"` (для користувачів qBittorrent Remote Lite введіть `curl --form-string "message=%N завантаження завершено" "https://qbpushlite.fengmlo.com/api/v1/push/ваш-користувач"`) у розділі "Запускати зовнішню програму" полі "Запущений торрент завершений", натисніть "Зберегти"

Для прикладу, для користувача `abc123`, команда буде виглядати так:

```bash
curl --form-string "message=%N завантаження завершено" "https://qbpush.fengmlo.com/api/v1/push/abc123"
```

Готово!
