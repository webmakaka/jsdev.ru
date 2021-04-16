# [jsdev.ru](https://jsdev.ru) source codes

<br/>

### Запустить jsdev.ru на своем хосте с использованием docker-compose (для работы над проектом):

    $ docker-compose up

<br/>

Остается подключиться к localhost  
Порт подключения 80

<br/>

### Запустить jsdev.ru на своем linux хосте как сервис

    # vi /etc/systemd/system/jsdev.ru.service

Insert code from jsdev.ru.service

    # systemctl enable jsdev.ru.service
    # systemctl start jsdev.ru.service
    # systemctl status jsdev.ru.service

http://localhost:4017

<br/><br/>

---

<br/>

**Marley**

Any questions in english: <a href="https://jsdev.org/chat/">Telegram Chat</a>  
Любые вопросы на русском: <a href="https://jsdev.ru/chat/">Телеграм чат</a>
