# BioTime8.0 README

## Code Structure
Pass

## Run BioTime8.0 in Development
1. Environmental preparation
    + python env
        - get python env in [svn](http://time-svn.xmzkteco.com/svn/BioTime/BioTimePythonEnv/Python27)
        - activate python env  
        edit init.bat file, and make config it can activate your python env
        ```
        init.bat
        python -V
        python -m pip -V
        ```
    + sql database  
        create a database and make sure the database can be connected  
        config it in .../trunk/attsit.ini file like:
        ```
        [DATABASE]
        ENGINE=mysql
        NAME=biotime8
        USER=root
        PASSWORD=password
        PORT=3306
        HOST=127.0.0.1
        ```
    + redis  
        make sure you has install redis  
        you can also insall redis-desktop-manager(0.8.8) to test conn  
        config it in .appconfig file:
        ```
        [REDIS]
        REDIS_HOST = 127.0.0.1
        REDIS_PORT = 6379
        REDIS_PASSWORD =
        [CELERY]
        ACTIVE_CELERY = 1
        CELERY_BROKER_DB = 1
        CELERY_RESULT_DB = 2
        ```
    + memcached  
        make sure you has install memcached  
        just run memcached.exe  
        or you can add it into Windous Scheduled Tasks

2. make migrtions&migrate  
    you can do all operations in migrations_helper.bat
    ```
    python manage.py makemigrations
    python manage.py migrate
    ```
3. runserver  
    biotime8.0 use celery get communication from device, so you need runserver and run redis
    ```
    make sure memcached running
    python manage.py runserver 0.0.0.0:8081
    # Asynchronous task and device communication need celery worker
    python manage.py celery worker -c 1 --loglevel=info
    # periodic task need run celery beat
    python manage.py celery beat
    ```


## pack a windous package
Pass


## install biotime8.0 with windous package
1. installation
    if install success, biotime8.0 will has install  service
    + ...
    + ...
    + ...


## code format
- [pep8](https://www.python.org/dev/peps/pep-0008/), [pep8 Chinese translation](https://python.freelycode.com/contribution/detail/47), [pep8 Chinese translation](https://blog.csdn.net/ratsniper/article/details/78954852)

- Use python2.7 python3.x compatible syntax
    - **print**
        ```
        # good
        print('...')

        # bad
        print '...'
        ```

    - **dict.has_key() dict.keys()**
        ```
        # good
        for key in dict:
            pass
        if key in dict:
            pass

        # bad, python3 run error
        if dict.has_key('key'):
            pass
        ```

    - **try ... except...**
        ```
        # good
        try:
            pass
        except Exception as e:
            pass

        # bad, python3 run error
        try:
            pass
        except Exception, e:
            pass
        ```

    - **relative path import**
        ```
        # good
        from .folder.foo import bar

        # bad
        from folder.foo import bar
        ```

    - **xrange**
        ```
        # python3 alias xrange to range
        ```

    - **file()**
        ```
        # good
        with open() as f:
            pass

        # bad, python3 run error
        f = file()
        f.close()
        ```

- code suggestion
    - **import**
        ```
        # Standard library import
        # Related third-party library import
        # Local app/library specific import
        # You should add a blank line between each group of imports.
        # Do not use from package import *
        # Reduce the use of import in the function

        import os
        import json

        from django.conf import setting
        from package import fuction

        form mysite import utils
        from .folder imort some_file
        ```

    - **None**
        ```
        # good
        if x is None:
            pass
        if x is not None:
            pass

        # bad
        if == None:
            pass
        if != None:
            pass
        ```

    - **multiple statements in multiple line**
        ```
        # good
        if foo == 'bar':
            pass

        # bad
        if foo == 'bar': pass
        ```