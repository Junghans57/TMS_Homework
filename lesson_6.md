## Задание 1
1) Получил список запланированных задач суперпользователя:
```bash
sudo crontab -l
```

2) Открыл файл crontab для редактирования:
```bash
sudo crontab -e
```
3) Добавил задание (строку в конец файла):
```cron
0 16 1 * * apt-get clean && apt-get autoclean
```
4) Проверил добавление задания:
```bash
sudo crontab -l
```
<img width="683" height="35" alt="image" src="https://github.com/user-attachments/assets/9a90e704-3152-48bf-ab95-e98d3226463d" />

## Задание 2
1) Установил nodejs:
```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
```
```bash
sudo apt-get install -y nodejs
```
2) Проверил правильность установки:
```bash
node -v
```
<img width="361" height="70" alt="image" src="https://github.com/user-attachments/assets/bf9e1034-99bd-4bd3-b071-cfc4e5daf7e5" />


3) Получил полный путь к nodejs:
```bash
which node
```
4) Добавил конфигурацию сервис-юнита (myapp.service) в директорию /etc/systemd/system:
```text
[Service]
Environment=MYAPP_PORT=3000
ExecStart=/usr/bin/node /usr/local/www/myapp/index.js
```
5) Создал директорию:
```bash
sudo mkdir -p /usr/local/www/myapp
```
6) Добавил скрипт с веб-сервером (index.js) в директорию из п.5:
```javascript
const http = require('http');
const MYAPP_PORT = process.env.MYAPP_PORT;

http.createServer((req, res) => {
	if(req.url === '/kill') {
		throw new ERROR('Someone kills me');
	}
	
	if(req.method === 'POST') {
		console.error(`Error: Request ${req.method} ${req.url}`);
		
		res.writeHead(405, {'Content-Type':'text/plain'});
		res.end('405 Method Not Allowed');
		
		return;
	}
	
	console.log(`Request ${req.method} ${req.url}`);
	
	res.writeHead(200, {'Content-Type':'text/plain'});
	res.end('200 OK');
}).listen(MYAPP_PORT);
```
7) Запустил сервис и проверил правильность запуска:
```bash
sudo systemctl start myapp.service
```
```bash
sudo systemctl status myapp.service
```
<img width="672" height="188" alt="image" src="https://github.com/user-attachments/assets/b3ad5b40-3414-4429-b094-036b7e83654a" />


8) Отправил GET-запрос для проверки работоспособности веб-сервера:
```bash
curl 'http://localhost:3000/'
```
<img width="489" height="39" alt="image" src="https://github.com/user-attachments/assets/43de593c-1a5f-449d-b10e-67feae12b1cd" />


9) Добавил в конфигурацию сервис-юнита строку для автоматического перезапуска сервиса:
```text
Restart=always
```
10) Перезапустил юниты и сервис:
```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl restart myapp.service
```
11) Отправил GET-запрос, который приводит к остановке веб-сервера:
```bash
curl 'http://localhost:3000/kill'
```
12) Отправил GET-запрос для проверки работоспособности веб-сервера:
```bash
curl 'http://localhost:3000/'
```


13) Получил пользователя и группу, от имени которых запущен процесс:
```bash
sudo systemctl show -p MainPID myapp.service | cut -d'=' -f2 | xargs -I{} ps -o user,group -p {}
```



14) Добавил в конфигурацию сервис-юнита строки для настройки пользователя и группы, от имени которых будет запущен процесс:
```bash
User=tms-user
Group=tms-user
```
15) Перезапустил юниты и сервис
16) Проверил изменение пользователя и группу, от имени которых запущен процесс:
```bash
sudo systemctl show -p MainPID myapp.service | cut -d'=' -f2 | xargs -I{} ps -o user,group -p {}
```
<img width="921" height="66" alt="image" src="https://github.com/user-attachments/assets/54a20c53-f7e5-4742-9d71-50fccd89fbf5" />


17) Просмотрел логи в журнале systemd:
```bash
journalctl -u myapp.service
```
<img width="925" height="1355" alt="image" src="https://github.com/user-attachments/assets/5a8508d7-a175-4864-8a6d-f279a239d005" />

Победить ощибку не удалось(Вывод:

systemd с сервисом всё ок, он перезапускает падения.

Основная проблема — ошибка в Node.js: throw new Error('Someone kills me'). Надо править логику обработки POST-запросов в index.js.

Мелкие предупреждения systemd (Stan>) можно проигнорировать, но лучше глянуть строки 11–12 юнита.)

18) Добавил в конфигурацию сервис-юнита строки для настройки вывода процесса в syslog:
```text
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=myapp
```
19) Добавил конфигурацию syslog-демона (rsyslog) (100-myapp.conf) для настройки правил обработки логов (syslog) в директорию /etc/rsyslog.d/:
```text
$RepeatedMsgReduction off
if $programname=='myapp' then -/var/log/myapp/debug.log
```
20) Перезапустил юниты, rsyslog и сервис:
```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl restart rsyslog.service
```
```bash
sudo systemctl restart myapp.service
```
21) Просмотрел логи в syslog:
```bash
sudo cat /var/log/myapp/debug.log
```
<img width="586" height="179" alt="image" src="https://github.com/user-attachments/assets/c4f75499-4197-426f-9a45-1d9730c68446" />


22) Изменил конфигурацию сервис-юнита для вывода в разные файлы (в зависимости от уровня severity):
```text
[Service]
Environment=MYAPP_PORT=3000
ExecStart=/bin/sh -c '/usr/bin/node /usr/local/www/myapp/index.js | logger --tag myapp'
Restart=always
User=tms-user
Group=tms-user
StandardError=syslog
SyslogIdentifier=myapp
SyslogLevel=err
```
23) Изменил конфигурацию syslog-демона (100-myapp.conf) для вывода в разные файлы (в зависимости от уровня severity):
```text
$RepeatedMsgReduction off
if $programname=='myapp' and $syslogseverity < 5 then -/var/log/myapp/error.log
if $programname=='myapp' and $syslogseverity >= 5 then -/var/log/myapp/debug.log
```
24) Перезапустил юниты, rsyslog и сервис
25) Отправил GET-запрос и POST-запрос:
```bash
curl 'http://localhost:3000/'
```
```bash
curl -X POST http://localhost:3000/
```
26) Просмотрел логи в разных файлах:
```bash
sudo cat /var/log/myapp/debug.log
```
```bash
sudo cat /var/log/myapp/error.log
```

