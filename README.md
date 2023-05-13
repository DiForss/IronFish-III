# IronFish-III
nodes
Гайд по установке ноды IronFish

IronFish — это блокчейн первого уровня, который станет универсальным уровнем конфиденциальности для web3. Используя доказательства с нулевым разглашением (zk-SNARK) и высочайшие стандарты шифрования, блокчейн даст пользователям возможность проводить полностью приватные транзакции.

Проект собрал $32.9 млн от a16z, Sequoia Capital, Electric Capital, Slow Ventures, Alan Howard и других.

18 января команда запустила третью фазу тестнета, в котором нужно зарабатывать поинты за различные задания: нода, минт/сжигание/отправка токенов и поиск багов, чтобы продвигаться в лидерборде.

Все команды для установки ноды, и для заданий, чтобы получать поинты вы найдете в этом гайде.

Аренда сервера
Арендуем сервер, например на Contabo. Рекомендуемые характеристики для IronFish: 4 CPU, 8 GB RAM и операционная система ubuntu 20.04. Можете подселить к другим нодам.

При оплате сервера необходимо ввести пароль, с помощью которого вы будете подключаться к серверу. После покупки вам на почту придет письмо с данными вашего сервера.

Подключение к серверу
Для того, чтобы подключиться к серверу на Windows потребуется программа PuTTY.

В “Host Name” вводим IP вашего сервера и нажимаем “Open”;
В открывшимся окне прописываем команду: root;
Жмем “Enter” и вставляем пароль от сервера, затем “Enter”.
На MacOS просто запускаем программу Terminal.

Заходим на сервер командой: ssh root@IP_ADDRESS, IP_ADDRESS меняем на IP сервера;
Дальше вводим “yes”, жмем “Enter” и вставляем пароль от сервера (введеный пароль будет скрыт иконкой с ключом). Жмем “Enter”.
Установка ноды
Установку мы взяли у ребят из Nodes Guru. Официальная статья по ссылке.

Выполняем команды на сервере:

sudo apt update
sudo apt full-upgrade
wget -q -O ironfish.sh https://api.nodes.guru/ironfish.sh && chmod +x ironfish.sh && ./ironfish.sh && unalias ironfish 2>/dev/null
Выбираем полную установку: вводим 1 и дальше пишем желаемое имя кошелька, ноды и кол-во ядер на вашем сервере.

Останавливаем майнер командой:

service ironfishd-miner stop
Изначально у нас устанавливается нода и майнер. Майнер нужен, чтобы нам капали токены IRON, но он будет полностью нагружать наш сервер, поэтому будем клянчить токены в чате.

Теперь создаем кошелек:

ironfish wallet:create $IRONFISH_WALLET
Вас попросит ввести желаемое имя кошелька, можете ввести такое же, как писали выше при установке.

Устанавливаем кошелек по-умолчанию:

ironfish wallet:use $IRONFISH_WALLET
Проверять адрес и баланс вашего кошелька можно командами:

ironfish wallet:address
ironfish wallet:balance
Наша главная цель этого тестнета — набить как можно больше поинтов, чтобы подняться в лидерборде. Для этого нужно раз в неделю минтить, сжигать и отправлять токены.
Место можно смотреть в лидерборде по ссылке, обязательно регистрируемся и указываем правильное имя ноды/граффити, посмотреть свое имя можно командой:

cat $HOME/.ironfish/config.json
Идем клянчить токены в чат проекта: например в Discord канале или Telegram чате. Как упоминали выше, адрес вашего кошелька можно проверить командой:

ironfish wallet:address
Затем проверяем баланс вашего кошелька и когда отправят токены приступаем к дальнейшим действиям. Проверить баланс можно командой:

ironfish wallet:balance
Также включаем телеметрию, чтобы нам капали поинты за ноду:

ironfish config:set enableTelemetry true
Еженедельные задания
Теперь переходим к минту нового токена, его сжиганию и к отправке. Минтим новый токен командой:

ironfish wallet:mint --name=ВАШ_ГРАФФИТИ
Если забыли граффити, можно проверить командой:

cat $HOME/.ironfish/config.json
Вводим ваш граффити еще раз, указываем любое желаемое кол-во токенов, вводим минимальную комиссию: 0.00000001 и затем нажимаем Y.

Ждем пару минут и сжигаем половина токенов командой:

ironfish wallet:burn
Выбираем токен, вводим половину от кол-ва, которое вы создали и вводим минимальную комиссию: 0.00000001.

Ждем пару минут и переходим к отправке. Отправлять токены нужно только на 1 адрес: dfc2679369551e64e3950e06a88e68466e813c63b100283520045925adbe59ca

Вводим команду:

ironfish wallet:send --to dfc2679369551e64e3950e06a88e68466e813c63b100283520045925adbe59ca
Выбираем токен, который вы сминтили, ставим минимальную комиссию: 0.00000001 и отправляем. Таким же действием вы можете кому-то помочь и отправить токены IRON, подставив адрес пользователя и выбрав токен IRON.

Через определенное время можете проверить себя в лидерборде, вам должны засчитать уже 600 поинтов.

Повторимся, что вам нужно будет минтить, сжигать и отправлять токены каждую неделю, чтобы зарабатывать очки и продвигаться в лидерборде.

Обновление v0.1.67
Выполняем команду и нажимаем 2 (Upgrade):

wget -q -O ironfish.sh https://api.nodes.guru/ironfish.sh && chmod +x ironfish.sh && sudo /bin/bash ironfish.sh
Останавливаем майнер:

service ironfishd-miner stop
А также выполняем команды:

sudo systemctl stop ironfishd
ironfish migrations:start
sudo systemctl restart ironfishd
Trusted Setup
Это ключевой шаг на пути к майнет, церемония будет длиться с 13 февраля до 3 марта. Для участия выполняем команды:

npm install -g ironfish
Проверяем, чтобы версия была 65+, если нет выполняем обновление ноды из раздела выше.

ironfish --version
screen -S ironfish
ironfish ceremony
Нажимаем Enter, теперь вводим свое имя и еще раз нажимаем Enter. Дальше можем выйти из скрина с помощью ctrl+A+D или control+A+D на MacOS. Терминал можно закрывать, вы все равно будете оставаться в очереди, чтобы открыть еще раз скрин, вводим команду:

screen -R ironfish
После того, как дойдет ваша очередь, обязательно сохраняем цифровой код.

Полезные команды
Проверить логи:

journalctl -u ironfishd -f
Список всех доступных команд с кошельком:
ironfish wallet
g




