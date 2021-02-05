# Создание самоподписанных сертификатов SSL для Apache в (Debian based) Linux

На основе [digitalocean.com Tutorials](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-18-04-ru)

Самоподписанный сертификат шифрует данные, которыми ваш сервер обменивается с любыми клиентами. Однако поскольку он не подписан доверенным центром сертификации из числа встроенных в браузеры, пользователи не могут использовать этот сертификат для автоматической проверки подлинности вашего сервера.

Самоподписанный сертификат полезен в ситуациях, когда у вашего сервера нет доменного имени, а также в случаях, когда шифрованный веб-интерфейс не предназначен для взаимодействия с пользователями. Если у вас есть доменное имя, в большинстве случае будет полезнее использовать сертификат, подписанный центром сертификации. Например, [здесь](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-18-04) вы можете узнать, как создать бесплатный доверенный сертификат с помощью проекта **Let’s Encrypt**.

- [Шаг 1 – Создание сертификата SSL](#ssl_create)
- [Шаг 2 — Настройка Apache для использования SSL](#apache_config)
  - [Создание сниппета конфигурации Apache с надежными настройками шифрования](#ssl_snippet)
  - [Изменение файла виртуального хоста Apache SSL по умолчанию](#virtual_host)
  - [(Рекомендуется) Изменение файла хоста HTTP для перенаправления на HTTPS](redirect_to_https)
- [Шаг 3 — Настройка брандмауэра (firewall)](<#firewall_adjusting)
- [Шаг 4 — Активация изменений в Apache](apache_activate)
- [Шаг 5 — Проверка работы шифрованого соединения](check_ssl)
  - [Особенности поведения браузера в случае с самоподписанными сертификатами](browser_features)


<a name="ssl_create"></a>
# Шаг 1 – Создание сертификата SSL

:bangbang: <small>В качестве примера, я создаю самоподписанный сертификат для локальной версии проекта Auto.Kazka. Я планирую подключить и некоторые другие свои виртуальные хосты через https, поэтому, в данной инструкции ключи я называю по имени проекта: `apache-autokazka`. В оригинальной статье (ссылка выше) речь идет только об одном хосте.</small>

Протоколы TLS и SSL используют сочетание открытого сертификата и закрытого ключа. Секретный ключ SSL хранится на сервере. Он используется для шифрования отправляемых на клиентские системы данных. Сертификат SSL находится в открытом доступе для всех, кто запрашивает этот контент. Его можно использовать для расшифровки контента, подписанного соответствующим ключом SSL.

Мы можем создать самоподписанный ключ и пару сертификатов OpenSSL с помощью одной команды:

`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-autokazka.key -out /etc/ssl/certs/apache-autokazka.crt`

Вам будет предложено ответить на ряд вопросов. Прежде чем перейти к этому шагу, посмотрим, что делает отправляемая нами команда:

- **openssl**: это базовый инструмент командной строки для создания и управления сертификатами OpenSSL, ключами и другими файлами.
- **req**: данная субкоманда указывает, что мы хотим использовать управление запросами подписи сертификатов X.509 (CSR). X.509 — это стандарт инфраструктуры открытых ключей, используемый SSL и TLS для управления ключами и сертификатами. Вы хотим создать новый сертификат X.509, и поэтому используем эту субкоманду.
- **-x509**: это дополнительно изменяет предыдущую субкоманду, сообщая утилите, что мы хотим создать самоподписанный сертификат, а не сгенерировать запрос на подпись сертификата, как обычно происходит.
- **-nodes**: этот параметр указывает OpenSSL пропустить опцию защиты сертификата с помощью пароля. Для чтения этого файла при запуске сервера без вмешательства пользователя нам потребуется Apache. Кодовая фраза может предотвратить это, поскольку нам придется вводить ее после каждого перезапуска.
- **-days 365**: данный параметр устанавливает срок, в течение которого сертификат будет считаться действительным. Здесь мы устанавливаем срок действия в один год.
- **-newkey rsa:2048**: указывает, что мы хотим генерировать новый сертификат и новый ключ одновременно. Мы не создали требуемый ключ для подписи сертификата на предыдущем шаге, и поэтому нам нужно создать его вместе с сертификатом. Часть rsa:2048 указывает, что мы создаем ключ RSA длиной 2048 бит.
- **-keyout**: эта строка указывает OpenSSL, где мы разместим создаваемый закрытый ключ.
- **-out**: данный параметр указывает OpenSSL, куда поместить создаваемый сертификат.

```
[sudo] password for olex: 
Can't load /home/olex/.rnd into RNG
140352258798016:error:2406F079:random number generator:RAND_load_file:Cannot open 
file:../crypto/rand/randfile.c:88:Filename=/home/olex/.rnd
Generating a RSA private key
......................................+++++
....+++++
writing new private key to '/etc/ssl/private/apache-autokazka.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
```

Как мы указывали выше, эти опции создают и файл ключа, и сертификат. Нам будет задано несколько вопросов о нашем сервере, чтобы правильно вставить информацию в сертификат.

Укажите подходящие ответы. Самая важная строка — это строка, где запрашивается обычное имя (т. е. FQDN сервера или ВАШЕ имя). Вам нужно ввести доменное имя, связанное с вашим сервером или, что более вероятно, публичный IP-адрес вашего сервера.

В целом, диалог выглядит примерно так:

```
Country Name (2 letter code) [AU]:UA
State or Province Name (full name) [Some-State]:Kyiv Obl.
Locality Name (eg, city) []:Kyiv
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Auto.Kazka  
Organizational Unit Name (eg, section) []:OlexSyn        
Common Name (e.g. server FQDN or YOUR name) []:auto.kazka.org.ua.loc
Email Address []:myemail@gmail.com
```
Оба созданных вами файла будут помещены в соответствующие подкаталоги в каталоге /etc/ssl:
- `/etc/ssl/private/apache-autokazka.key`  (эта директория закрыта, зайти можно только под root'ом)
- `/etc/ssl/certs/apache-autokazka.crt`  (а в этой вообще целая свалка различных сертификатов `.pem`!.. Серт.центры?)

<a name="apache_config"></a>
## Шаг 2 — Настройка Apache для использования SSL

Мы создали файлы ключа и сертификата в каталоге `/etc/ssl`. Теперь нам нужно изменить конфигурацию Apache, чтобы воспользоваться ими.

1. Создадим сниппет конфигурации, чтобы задать надежные параметры SSL по умолчанию.
2. Мы изменим входящий в комплект файл виртуального хоста SSL Apache, чтобы он указывал на сгенерированные нами сертификаты SSL.
3. (Рекомендуется) Мы изменим незашифрованный файл виртуального хоста, чтобы он автоматически перенаправлял запросы на шифрованный виртуальный хост.

После завершения настройки мы получим защищенную конфигурацию SSL.

<a name="ssl_snippet"></a>
### Создание сниппета конфигурации Apache с надежными настройками шифрования

Прежде всего, мы создадим сниппет конфигурации Apache для определения некоторых параметров SSL. При этом в Apache будет настроен надежный пакет шифров SSL и будут включены расширенные функции, которые обеспечат безопасность нашего сервера. Настраиваемые нами параметры смогут использовать любые виртуальные хосты с SSL.

Создайте новый сниппет в каталоге /etc/apache2/conf-available. Мы назовем файл ssl-params.conf, чтобы сделать его назначение очевидным:

`sudo nano /etc/apache2/conf-available/ssl-params.conf`

Для наших целей мы скопируем предоставленные настройки полностью. Мы внесем только одно небольшое изменение. Мы отключим заголовок Strict-Transport-Security (HSTS).

Вставьте конфигурацию в открытый нами файл **ssl-params.conf**:

```apache
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLHonorCipherOrder On
# Disable preloading HSTS for now.  You can use the commented out header line that includes
# the "preload" directive if you understand the implications.
# Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff
# Requires Apache >= 2.4
SSLCompression off
SSLUseStapling on
SSLStaplingCache "shmcb:logs/stapling-cache(150000)"
# Requires Apache >= 2.4.11
SSLSessionTickets Off
```

Сохраните файл и закройте его после завершения.

<a name="virtual_host"></a>
### Изменение файла виртуального хоста Apache SSL по умолчанию

Теперь изменим конфигурацию хоста проекта `/etc/apache2/sites-available/auto_kazka_org_ua.conf`. Строки, добавленные к стандартной конфигурации для работы ssl я пометил как `# ssl`:

```apache
<IfModule mod_ssl.c>                                                   # ssl
    <VirtualHost 127.0.1.77:443>                                       # ssl Внимание! Здесь порт `:80` надо заменить на `:443`!
        ServerName auto.kazka.org.ua.loc
        DocumentRoot /home/olex/www/kazka/auto.kazka.org.ua

        SSLEngine on                                                   # ssl
        SSLCertificateFile     /etc/ssl/certs/apache-autokazka.crt     # ssl
        SSLCertificateKeyFile  /etc/ssl/private/apache-autokazka.key   # ssl

        <FilesMatch "\.(py|html|htm|css|js)$">                         # ssl  # все? а картинки?
            SSLOptions +StdEnvVars                                     # ssl
        </FilesMatch>                                                  # ssl

        <Directory /home/olex/www/kazka/auto.kazka.org.ua/>
            Options +Includes
            AddType text/html .htm
            AddOutputFilter INCLUDES .htm
            AllowOverride All
            Require all granted
        </Directory>

        ScriptAlias /cgi-bin/ /home/olex/www/kazka/cgi-bin/
        <Directory "/home/olex/www/kazka/cgi-bin">
            AllowOverride None
            Options +ExecCGI -MultiViews
            Require all granted
            # see https://olexsyn.github.io/e-note/apache/cgi-utf-fix/
            PassEnv LANG en_US.UTF-8
            SSLOptions +StdEnvVars                                     # ssl
        </Directory>

        ErrorLog /home/olex/www/__logs/kazka_auto/error.log
        CustomLog /home/olex/www/__logs/kazka_auto/access.log combined

    </VirtualHost>
</IfModule>                                                            # ssl
```

<a name="redirect_to_https"></a>
### (Рекомендуется) Изменение файла хоста HTTP для перенаправления на HTTPS

В настоящее время сервер будет предоставлять нешифрованный трафик HTTP и шифрованный трафик HTTPS. В большинстве случаев для обеспечения безопасности рекомендуется включить автоматическое перенаправление HTTP на HTTPS. Если вы не хотите использовать эту функцию, или она вам не нужна, вы можете спокойно пропустить этот раздел.

Я - не делал. Чтобы при раработке видеть, что ссылка привела на незащищенное соединение. На сервере это делаю в файле **.htaccess**

<a name="firewall_adjusting"></a>
## Шаг 3 — Настройка брандмауэра (firewall)

Не делал. Его у меня нет. Если понадобится - ссылка вначале статьи.

<a name="apache_activate"></a>
## Шаг 4 — Активация изменений в Apache

Теперь нужно включить в Apache модули SSL и заголовков, активировать наш виртуальный хост SSL и перезапустить Apache.

Мы можем активровать `mod_ssl` и `mod_headers` - модули Apache, необходимые для некоторых настроек нашего сниппета SSL, с помощью команды `a2enmod`:

```
sudo a2enmod ssl
sudo a2enmod headers
```

Теперь мы можем активировать сниппет SSL и сам виртуальный хост (если не сделали этого раньше) с помощью команды a2ensite:

```
sudo a2enconf ssl-params
sudo a2ensite auto_kazka_org_ua
```
 
Мы активировали наш сайт и все необходимые модули. Теперь нам нужно проверить наши файлы на наличие ошибок в синтаксисе. Для этого можно ввести следующую команду:

```
sudo apache2ctl configtest
Syntax OK
```
Если в конфигурации нет синтаксических ошибок, мы можем безопасно перезапустить Apache для внесения изменений:

```
sudo systemctl restart apache2`
```

<a name="check_ssl"></a>
## Шаг 5 — Проверка работы шифрованого соединения

Теперь мы готовы протестировать наш сервер SSL.

Откройте браузер и введите https:// и доменное имя или IP-адрес вашего сервера в адресную панель:

`https://auto.kazka.org.ua.loc`

<a name="browser_features"></a>
### Особенности поведения браузера в случае с самоподписанными сертификатами]

Поскольку созданный нами сертификат не подписан одним из доверенных центров сертификации вашего браузера, вы увидите пугающее предупреждение:

Такое предупреждение нормально, и его следует ожидать. Сертификат нам нужен только для шифрования, а не для подтверждения подлинности нашего хоста третьей стороной. Нажмите «Дополнительно», а затем нажмите на указанную ссылку, чтобы перейти к своему хосту:

Обход предупреждения о самоподписанном сертификате Apache

Теперь должен открыться ваш сайт. Если вы посмотрите в адресную строку браузера, вы увидите символ замка со знаком «x». В данном случае это означает, что сертификат не удается проверить. Ваше соединение все равно шифруется.

Если вы настроили Apache для перенаправления HTTP на HTTPS, вы можете проверить правильность перенаправления функций:

http://server_domain_or_IP
Если при этом появляется такой же значок, перенаправление работает правильно.


