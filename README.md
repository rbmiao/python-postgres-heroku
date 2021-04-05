# Heroku is kinda SaaS provider

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

### Heroku Deployment Steps

https://gist.github.com/bradtraversy/0029d655269c8a972df726ed0ac56b88


## Reference: 
https://www.youtube.com/watch?v=w25ea_I89iM&t=2470s
