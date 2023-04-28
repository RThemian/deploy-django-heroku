# Deploy to Heroku:
## first commands in the CLI
1. heroku login 
2. pip install django-heroku
3. pip install gunicorn 
## catcollector/settings.py -- at the bottom
# configure django to work within heroku environment
1. import django_heroku
2. django_heroku.settings(locals())

## touch a file "Procfile"
# in the file:
//starts the web process that runs the Django project
1. web: gunicorn catcollector.wsgi 

## in CLI 
1. pip freeze > requirements.txt // outputs dependencies to new file
2. heroku create < project_name >
// make a commit and push
3. git push heroku main
// add all of the secret keys to via
4. heroku config:set AWS_ACCESS_KEY_ID="MADE_UP_KEY"
// any others
// if error with django secret key, recreate django secret key
// commit and push to heroku
## in settings.py
5. ALLOWED_HOSTS = ['*'] #sets up CORS 
// or you can use your specific heroku url
// ALLOWED_HOSTS = ['https://catcollector-nov8.herokuapp.com/']
// diagnose issues with 
6. heroku logs --tail

//create bit.io database
//connect
## in settings.py 
7. replace DATABASES from Connect info
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'RThemian/catcollector-nov8',
        'USER': os.environ['USER'],
        'PASSWORD': os.environ['PASSWORD'],
        'HOST': 'db.bit.io',
        'PORT': '5432',
    }
}

## in CLI
1. heroku addons --all
2. heroku addons:destroy <YOUR OWN postgresql-encircled-74075 >
