# Проблема с SSI в связке Apache и Nginx на Mirohost

### Проблема

SSI корректно работает только на ссылках типа

`example.com/test/`

а на страницах

`example.com/test/index.htm`  
`example.com/test/something.htm`

не работает

### Решение

В панели управления Mirohost, разделе "Сервер" - "Настройки Nginx" добавить в "Расширения файлов, которые не будут отдаваться как статические файлы nginx'ом" расширение `htm`.

### Keys

<button>mirohost</button> <button>ssi</button> <button>apache</button> <button>nginx</button>
