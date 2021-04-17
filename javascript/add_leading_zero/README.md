# Добавить текущий ноль

Просто добавьте ведущий 0 каждый раз, затем используйте slice(-2), чтобы получить последние два символа, например:

```javascript
('0' + currentDate.getHours()).slice(-2)
```
[Подробнее про slice...](https://learn.javascript.ru/string#poluchenie-podstroki)


### Вставляємо дату у поле вводу

html:

```html
<div>
    <label>Дата реєстрації</label>
    <input type="text" id="tRegDt" value="{{ REGDT }}" />
</div>

<div>
    <input type="button" id="bToday" value="Сьогодні" />
</div>
```

javascript:

```javascript
    $("#bToday").click(function(e)
    {
        e.preventDefault();
        let today = new Date();
        let date_str =  today.getFullYear() + '-' +
                ('0' + (today.getMonth() + 1)).slice(-2) + '-' +
                ('0' +  today.getDate()      ).slice(-2);
        $("#tRegDt").val(date_str);
    });
```
