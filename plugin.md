## Документация по написанию плагинов для сервера

###### Загрузить чат и сервер можно с [репозитория](https://github.com/Danilus-s/DanilusChat)

Для начала работы требуется импортировать библиотеку **_sfuncs_**

`import sfuncs`

`client` - это дескриптор для взаимодействия с подключенными клиентами

Для инициации плагина, создайте класс `Plugin`:

__Пример__:

`plugin = sfuncs.Plugin("имя", "автор", "версия")`

Чтобы получить информацию о плагине, используйте функцию get_info() плагина, учтите что эта функция возвращает всё кроме команд.

`plugin_info = plugin.get_info()`

Получить все команды:

`cmds = plugin.get_commands()`

Создать команду:

```py
@plugin.command("имя", "описание")
def function(args, cln):
  # код
```

`args` - аргументы (если нет, равен `[]`)

`cln` - сокет отправителя

Создать коллбэк:

```py
def functioninit():
  # код выполнимый при запуске сервера

plugin.set_callback(functioninit, "init")
```

`"init"` - название коллбэка

### Доступные (и полезные) функции

- `getClients() -> dict` возвращает словарь подключенных клиентов

  Аналог `clients = sfuncs.clients `

- `log(fro, message) -> None` пишет `message` в консоль сервера и записывает в лог в формате `[12:12:12] <fro> message`

- `broadcast(message) -> None` рассылает `message` всем подключенным клиентам

- `listJoin(org_list, seperator=' ') -> str` объединяет элементы массива в строку

- `removeFormat(text) -> str` полностью удаляет форматирование

- `removeFont(text) -> str` удаляет форматирование, связанное с модификацией шрифта

- `send(client, message)` отправляет `client` сообщение с текстом `message`, используйте эту функцию, так как она сама шифрует сообщение
  
- `banNick(nick) -> None` бан по нику

- `banIP(ip) -> None` бан по IP

- `unbanNick(nick) -> None` разбан по нику

- `unbanIP(ip) -> None` разбан по IP

- `getBan(nick, addr) -> bool` проверяет, забанен ли пользователь по IP/нику

- `canSend: bool` по умолчанию True, если False сервер не будет обрабатывать полученное сообщение (сообщение не будет отправлено всем, а команда не будет исполнена)

### Калбэки (callback)

- Структура `data`
  - `data[0]` - `client`
  - `data[1]` - `message`

- `newUser(data)` вызывается когда подключается новый пользователь
- `receive(data)` вызывается когда кто-то отправляет сообщение
- `init()` вызывается единожды при запуске сервера



###### meow
