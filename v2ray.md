Установка под войд
Чтобы узнать список нужных пакетов
```
curl -s https://api.github.com/repos/v2rayA/v2rayA/releases/latest \           
  | grep '"browser_download_url"' | grep linux_x64       
```
Веб морда
```
curl -fL \                                                                     
  https://github.com/v2rayA/v2rayA/releases/download/v2.4.11/v2raya_linux_x64_2.4.11 \
  -o v2raya

sudo install -Dm755 v2raya /usr/local/bin/v2raya    
```
Ядро приложения
```
cd /tmp                                                                   

curl -fL \
  https://github.com/v2rayA/v2rayA/releases/download/v2.4.11/v2raya_core_linux_x64_2.4.11 \
  -o v2raya_core

sudo install -Dm755 v2raya_core /usr/local/bin/v2raya_core
```
 Для обхода ошибки, приложение ожидает именно v2ray
```
sudo ln -sf /usr/local/bin/v2raya_core /usr/local/bin/v2ray #
```
Для запуска впн сервера у себя необходимо иметь v2ray_core и  v2rayA
v2rayA это веб морда для настройки сервера
через Бланк впн нужно зайти, получить ссылку на конфиг и вставить его в import веб морды
После для использования как прокси нужно настроить сервер (можно сокс5 прописать конфиг и добавить в группу прокси) добавить его впн сервер в группу прокси и нажать старт
в терминале 

### Запуск морды
```
sudo env V2RAYA_V2RAY_BIN=/usr/local/bin/v2ray \
/usr/local/bin/v2raya 
```

### Проверка портов
```
sudo ss -lntp | grep -E '20170|20171|20172' 
```

### Проверка связи
```
curl -v \                                                                                                              
  --proxy socks5h://127.0.0.1:20170 \
  --proxy-user 'ЮЗЕР:ПАРОЛЬ' \ # Пароль от пользователя добавленного проксе в веб морде
  https://example.com/ 
```
Или
```
 curl -v --proxy socks5h://127.0.0.1:20170 https://example.com/ 
```

В случае успешного успеха должно быть что то типа
```
> GET / HTTP/2
> Host: example.com
> User-Agent: curl/8.21.0
> Accept: */*
> 
* Request completely sent off
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
< HTTP/2 200 
< date: Fri, 14 Aug 2026 20:42:14 GMT
< content-type: text/html
< server: cloudflare
< last-modified: Wed, 12 Aug 2026 20:15:57 GMT
< allow: GET, HEAD
< accept-ranges: bytes
< age: 7769
< cf-cache-status: HIT
< cf-ray: a2b2c8f37dcc90cc-AMS
```
После можно развлекаться через эту проксю