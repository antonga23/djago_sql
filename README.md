# djago_sql
django app and conenct to database

1. 
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
2.
