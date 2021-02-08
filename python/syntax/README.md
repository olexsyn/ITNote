# Синтаксис

### перегорнути словник

```python
ip_dict = dict(
    '1.2.3.4' = 'server_1',
    '2.3.4.5' = 'server_2',
)
ip_dict = {v:k for k,v in ip_dict.items()}

print(ip_dict)
```
_output:_
```
{'server_1':'1.2.3.4','server_2':'2.3.4.5',}
```
