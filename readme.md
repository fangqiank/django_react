### 1.pip3 install  pipenv

### 2.pipenv shell

### 3.pipenv install django djangorestframework django-rest-knox

### 4.django-admin startproject leadmanager(project name)

### 5.python3 manage.py startapp leads

### 6.\leadmanager\settings.py->INSTALLED_APPS = []->add leads,rest_framework...

### 7.\leads.py -> add  models

  

```python
class Lead(models.Model):
    name=models.CharField(max_length=100)
    email=models.EmailField(max_length=100,unique=True)
    message=models.CharField(max_length=500,blank=True)
    created_at=models.DateTimeField(auto_now_add=True)
```

### 8.python3 manage.py makemigrations leads

### 9.python3 manage.py migrate

### 10.\leads-> create serializer.py

```python
from rest_framework import serializers
from leads.models import Lead

#Lead  Serializer

class LeadSerializer(serializers.ModelSerializer):
    class Meta:
        model=Lead
        fields='__all__'
```

### 11.\leads->create api.py

```python
from leads.models import Lead
from rest_framework import viewsets,permissions
from .serializer import LeadSerializer

# Lead Viewset

class LeadViewSet(viewsets.ModelViewSet):
    queryset=Lead.objects.all()
    permission_class=[
        permissions.AllowAny
    ]
    serializer_class=LeadSerializer
```

### 12.\leadmanager\urls

```python
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
    path('', include('leads.urls')),  
]
```

### 13.\leads-->create urls.py

```python
from rest_framework import routers
from .api import LeadViewSet

router=routers.DefaultRouter()
router.register('api/leads',LeadViewSet,'leads')

urlpatterns=router.urls
```

### 14.python3 manage.py runserver

### 15.python3 manage.py startapp frontend

### 16.create folders under /frontend

###   

```commonlisp
mkdir -p ./frontend/src/components
```

```commonlisp
mkdir -p ./frontend/{static,templates}/frontend
```

```
cd..

npm init -y

npm install -D webpack webpack-cli

npm i -D @babel/core babel-loader @babel/preset-env @babel/preset-react babel-plugin-transform-class-properties

npm i prop-types --save
```

