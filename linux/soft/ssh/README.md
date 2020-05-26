# SSH

{% include cl.htm cmd="ssh user@66.225.228.206" %}

или в **/home/user/.ssh/config**

```
Host a
    Hostname admin.mail-ua
    User mailua
Host root
    Hostname 66.225.228.206
    User root
Host user
    Hostname 66.225.228.206
```

и тогда так:

{% include cl.htm cmd="ssh a
ssh root
ssh user" %}
