# deploy-django-heroku
# Deploy to Heroku:
## first commands in the CLI
heroku login 
pip install django-heroku
pip install gunicorn 
## catcollector/settings.py -- at the bottom
# configure django to work within heroku environment
import django_heroku
django_heroku.settings(locals())

## touch a file "Procfile"
# in the file:
//starts the web process that runs the Django project
web: gunicorn catcollector.wsgi 

## in CLI 
pip freeze > requirements.txt // outputs dependencies to new file
heroku create < project_name >
// make a commit and push
git push heroku main
// add all of the secret keys to via
heroku config:set AWS_ACCESS_KEY_ID="MADE_UP_KEY"
// any others
// if error with django secret key, recreate django secret key
// commit and push to heroku
## in settings.py
ALLOWED_HOSTS = ['*'] #sets up CORS 
// or you can use your specific heroku url
// ALLOWED_HOSTS = ['https://catcollector-nov8.herokuapp.com/']
// diagnose issues with 
heroku logs --tail
