# Словари (dict)

## Создание пустого словаря:

```python
dict_sample1 = {}
dict_sample2 = dict()
```

## Создание словаря с данными:

Cловарь, где ключи являются целыми числами:

```python
dict_sample = {
    1: 'mango',
    2: 'banana'
}
```
Создание словаря с ключами разных типов:

```python
dict_sample = {
    'fruit': 'mango', 
    1: [4, 6, 8]
}
```

Можно также создать словарь, явно вызвав метод dict():

```python
dict_sample = dict(
    'one':'mango', 
    'two':'banana'
)
```
Чтобы код выглядел читабельней в dict() можно не использовать кавычки со строковыми ключами, но `:` при этом, нужно заменить знаком `=`:

```python
dict_sample = dict(
    one = 'mango',
    two = 'banana',  # у последней пары может стоять запятая
)
```

Словарь можно создать с помощью последовательности:

```python
dict_sample = dict(
    [(1,'mango'), (2,'banana')]
)
```

Словари могут быть вложенными. Это значит, что можно создавать словари внутри существующего словаря. Например:

```python
dict_sample = {
    1: {'student1': 'Nicholas', 'student2': 'John', 'student3': 'Mercy'}, 
    2: {'course1': 'Computer Science', 'course2': 'Mathematics', 'course3': 'Accounting'}
}
```

## Перебор словаря

```python
for k, v in dict_sample.items():
    print(k, '>', v)
```
```
one > mango
two > banana
```

## Перебор словаря по ключам

```python
for key in dict_sample.keys():
    print(key, '>', dict_sample[key])
```
```
one > mango
two > banana
```
## Перебор значений словаря

```python
for i in dict_sample.values():
    print(i)
```
```
mango
banana
```


{% include f.htm f="create.md" %}

