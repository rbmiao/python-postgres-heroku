# Heroku is a SaaS provider. 

# Python Feedback App

> Python Flask Feedback app that sends data to Postgres database and emails user

## Quick Start

Since pipenv uses python3 as default python,  although python3 has been set as default python, it still throw errors like:

```shell
Rongbings-MacBook-Pro:python_feedback_app rongbing$ pipenv shell
Warning: Python 3.7 was not found on your system...
Neither 'pyenv' nor 'asdf' could be found to install Python.
You can specify specific versions of Python with:

```


So providing python3 path can solve the problem:
```
Rongbings-MacBook-Pro:python_feedback_app rongbing$
Rongbings-MacBook-Pro:python_feedback_app rongbing$ pipenv --python /usr/local/bin/python3 shell
Creating a virtualenv for this project...
Pipfile: /Users/rongbing/python3/python_feedback_app/Pipfile
Using /usr/local/bin/python3 (3.9.1) to create virtualenv...
⠏ Creating virtual environment...created virtual environment CPython3.9.1.final.0-64 in 558ms
  creator CPython3Posix(dest=/Users/rongbing/.local/share/virtualenvs/python_feedback_app-qpr4Edyf, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/Users/rongbing/Library/Application Support/virtualenv)
    added seed packages: pip==21.0.1, setuptools==54.1.2, wheel==0.36.2
  activators BashActivator,CShellActivator,FishActivator,PowerShellActivator,PythonActivator,XonshActivator

```



```bash
# Add your DATABASE URI in app.py and your mail params in send_mail.py



# Install dependencies
pipenv shell
pipenv install

# Serve on localhost:5000
python app.py
```

## Sending emails uses mailtrap.io. 

## Online postgres database need to be created use 
```
(python_feedback_app) bash-3.2$ heroku run python
Running python on ⬢ miaolexusfeedback... up, run.9076 (Free)
Python 3.9.2 (default, Feb 19 2021, 15:57:12)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
>>> from  app import db
>>> db.create_all()
>>> exit()
(python_feedback_app) bash-3.2$
```

## git push files to heroku. Heroku starts building, installing, launching immediately
```
(python_feedback_app) bash-3.2$ git push heroku master
Enumerating objects: 23, done.
Counting objects: 100% (23/23), done.
Delta compression using up to 4 threads
Compressing objects: 100% (19/19), done.
Writing objects: 100% (23/23), 1.23 MiB | 1006.00 KiB/s, done.
Total 23 (delta 2), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Building on the Heroku-20 stack
remote: -----> Determining which buildpack to use for this app
remote: -----> Python app detected
remote: -----> Installing python-3.9.2
remote: -----> Installing pip 20.1.1, setuptools 47.1.1 and wheel 0.34.2
remote: -----> Installing dependencies with Pipenv 2020.11.15
remote:        Installing dependencies from Pipfile.lock (d3fb3d)...
remote: -----> Installing SQLite3
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote:
remote: -----> Compressing...
remote:        Done: 70.9M
remote: -----> Launching...
remote:        Released v5
remote:        https://miaolexusfeedback.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/miaolexusfeedback.git
 * [new branch]      master -> master
(python_feedback_app) bash-3.2$
```


### Heroku Deployment Steps

https://gist.github.com/bradtraversy/0029d655269c8a972df726ed0ac56b88



## Create online heroku database from local. (you must login to heroku first)
```
(python_feedback_app) bash-3.2$ heroku run python
Running python on ⬢ miaolexusfeedback... up, run.9076 (Free)
Python 3.9.2 (default, Feb 19 2021, 15:57:12)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
>>> from  app import db
>>> db.create_all()
>>> exit()
(python_feedback_app) bash-3.2$
```

## Before running app against database, login to online database to check:
```
(python_feedback_app) bash-3.2$ heroku pg:psql --app miaolexusfeedback
--> Connecting to postgresql-trapezoidal-49352
psql (13.1, server 13.2 (Ubuntu 13.2-1.pgdg20.04+1))
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
Type "help" for help.

miaolexusfeedback::DATABASE=> \d
                  List of relations
 Schema |      Name       |   Type   |     Owner
--------+-----------------+----------+----------------
 public | feedback        | table    | qzftoienbdxxxl
 public | feedback_id_seq | sequence | qzftoienbdxxxl
(2 rows)

miaolexusfeedback::DATABASE=> select * from feedback;
 id | customer | dealer | rating | comments
----+----------+--------+--------+----------
(0 rows)
```

## After running app on heroku, check database records from local:
```

miaolexusfeedback::DATABASE=> select * from feedback;
 id | customer  |    dealer     | rating |      comments
----+-----------+---------------+--------+--------------------
  1 | Worcester | Tom Smith     |     10 | He is very helpful
  2 | Miao      | Karen Swanson |      5 | He is pushy
(2 rows)

miaolexusfeedback::DATABASE=>
```

## sending email using mailtrap.io. You can find emails.

## If you got "500 Internal Error", it mostly is because username/password for database have been deleted. You need add them back.
```
ENV = 'prod'

if ENV == 'dev':
    app.debug = True
    app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://postgres@127.0.0.1/lexus'
else:
    app.debug = False
    app.config['SQLALCHEMY_DATABASE_URI'] = 'postgres://<Username>:<password>@$$$$$$$.amazonaws.com:5432/d6epceg0d6vbe5'
```


## If sending email failed, you need add username/password back to send_email.py
```
    login = ''
    password = ''
```


## Reference: 
https://www.youtube.com/watch?v=w25ea_I89iM&t=2470s

## Reference #2:
My Email: rbmiao
