# test

- [заголовок на кириллице](#title-on-cyrillic)

## [заголовок на кириллице](title-on-cyrillic)

```python
#-----------------------------------------------------------------------
def get_stroke_name(stroke_id, long=0):

    """
    Возвращает название стиля по его идентификатору stroke_id
    long=1, если необходимо длинное имя

    """
    if not stroke_id:  return _UNKNOWN

    if long:

        if   stroke_id == STROKE_FR:  res = 'вільний стиль'
        elif stroke_id == STROKE_FL:  res = 'батерфляй'
        elif stroke_id == STROKE_BR:  res = 'брас'
        elif stroke_id == STROKE_BA:  res = 'на спині'
        elif stroke_id == STROKE_IM:  res = 'комплексне пл.'
        else:                         res = _UNKNOWN

    else:

        if   stroke_id == STROKE_FR:  res = 'вс'
        elif stroke_id == STROKE_FL:  res = 'бт'
        elif stroke_id == STROKE_BR:  res = 'бр'
        elif stroke_id == STROKE_BA:  res = 'нс'
        elif stroke_id == STROKE_IM:  res = 'кп'
        else:                         res = _UNKNOWN

    return res

#def
```
