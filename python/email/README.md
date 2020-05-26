# Отправка email

<span class="r">TODO!</span> Проверь работу с `Cc:` и `Bcc:`

## Защищенное STARTTLS, с авторизацией на SMTP сервере

```python
import smtplib
from email.message import EmailMessage

smtp_serv = "smtp.example.com"
username  = "no-reply@example.com"
password  = "password"
from_mail = f"Mail Robot <{username}>"
reply_to  = "Support <support@example.com>"
to_mail   = "someuser@address.com"

msg = EmailMessage()
msg.set_content(body)

msg['Subject'] = subject
msg['From'] = from_mail
msg['To'] = to_mail
msg['Reply-to'] = reply_to

smtpObj = smtplib.SMTP(smtp_serv, 587)
# smtpObj.set_debuglevel(1)
smtpObj.starttls()
smtpObj.login(username, password)
smtpObj.send_message(msg)  # или smtpObj.sendmail(from, [to], body)
smtpObj.quit()
```

## Не защищенное, без авторизации

Иногда, если письмо необходимо переслать в пределах одного сервера (например, уведомление для администратора), авторизация не требуется.

```python
import smtplib
from email.message import EmailMessage

smtp_serv = "smtp.example.com"
username  = "no-reply@example.com"
from_mail = "Some Script <no-reply@example.com>"
to_mail   = "admin@example.com"

msg = EmailMessage()
msg.set_content(body)

msg['Subject'] = subject
msg['From'] = from_mail
msg['To'] = to_mail

smtpObj = smtplib.SMTP(smtp_serv)
smtpObj.send_message(msg)
smtpObj.quit()
```

## Links

- [Работа с почтой — модули email / smtplib](https://python-scripts.com/send-email-smtp-python)
- Perl: <http://ans.kiev.ua/wiki/perl/sendmail>, 
