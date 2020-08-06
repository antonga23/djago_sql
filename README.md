# djago_sql
django app and conenct to database

1. Creatae app and connect to database
```bash
$ install sql using brew
$ mkdir my_blog_app
$ cd my_blog_app
$ python3 -m venv env
$ . env/bin/activate
$ pip install django
$ django-admin startproject blog
$ cd blog
$ vim ~/my_blog_app/blog/blog/settings.py
$ add static root and IP to settings.py
$ STATIC_ROOT = os.path.join(BASE_DIR, 'static')
$ import os
$ python manage.py createsuperuser
$ brew install mysql-client 
$ echo 'export PATH="/usr/local/opt/mysql-client/bin:$PATH"' >> ~/.bash_profile
$ source ~/.bash_profile
$ pip install mysqlclient
$ sudo mysql -u root
$ > SHOW DATABASES;
$ > CREATE DATABASE blog_data;
$ > CREATE USER 'djangouser'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
$ > GRANT ALL ON blog_data.* TO 'djangouser'@'%';
$ > FLUSH PRIVILEGES;

replace database settings with :
    
          DATABASES = {
          'default': {
              'ENGINE': 'django.db.backends.mysql',
              'OPTIONS': {
                  'read_default_file': '/etc/mysql/my.cnf',
              },
          }
      }
$ vim/usr/local/opt/mysql/my.cnf
$ brew services start mysql
$ brew services stop mysql
$ brew services restart mysql

Test mysql connection:
$ python manage.py migrate
$ cd ~/my_blog_app/blog/
$ python manage.py runserver your-server-ip:8000
$ https://www.digitalocean.com/community/tutorials/how-to-create-a-django-app-and-connect-it-to-a-database
```
2. Add models to blog (https://www.digitalocean.com/community/tutorials/how-to-create-django-models)
```
$ cd ~/my_blog_app
$ . env/bin/activate
$ cd blog
$ python manage.py startapp blogsite
$ ls -la
$ cd ~/my_blog_app/blog/blogsite
$ cat models.py
$  We need to modify models.py
from django.db import models
from django.template.defaultfilters import slugify
from django.contrib.auth.models import User
from django.urls import reverse


class Post(models.Model):
    title = models.CharField(max_length=255)
    slug = models.SlugField(unique=True, max_length=255)
    content = models.TextField()
    created_on = models.DateTimeField(auto_now_add=True)
    author = models.TextField()

    def get_absolute_url(self):
        return reverse('blog_post_detail', args=[self.slug])

    def save(self, *args, **kwargs):
        if not self.slug:
            self.slug = slugify(self.title)
        super(Post, self).save(*args, **kwargs)

    class Meta:
        ordering = ['created_on']

        def __unicode__(self):
            return self.title


class Comment(models.Model):
    name = models.CharField(max_length=42)
    email = models.EmailField(max_length=75)
    website = models.URLField(max_length=200, null=True, blank=True)
    content = models.TextField()
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    created_on = models.DateTimeField(auto_now_add=True)
    
$
$
$

```
