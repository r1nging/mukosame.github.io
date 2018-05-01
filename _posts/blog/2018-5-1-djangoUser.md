---
layout: post
title: Django继承AbstractUser扩展User
category: blog
---

models.py
```Python
from django.db import models
from django.contrib.auth.models import AbstractUser

# Create your models here.
class User(AbstractUser):
	username=models.CharField(max_length=20,unique=True)
	password=models.CharField(max_length=30,default='')
```

admin.py

```
from django.contrib import admin
from TestModel.models import User

# Register your models here.
admin.site.register(User)

```

settings.py
```
AUTH_USER_MODEL = 'TestModel.User'
```

新建的User表字段要和内建User表一样。

创建出的管理员会在新建的User表里。