# Web Application Development:
## the_learning_log
### An online journal system that lets you keep track of information you've learned about a topic. Built using Django.  
<li>Features: </li>
  <ul>User authentication and robust security measures</ul>
  <ul>Optimized for performance, design, and functionality  </ul>
<li>Future Plans: </li>
  <ul>Containerize using Docker </ul> 
  <ul>Deploy to AWS </ul>  



# Some issues I worked through
<li>Duplicate 'staticfiles' Directories.</li>
  <ul>During some troubleshooting of the settings.py file, multiple static file directories were created. This caused a problem in the settings.py file identifying the correct path for the static files config.</ul>
  <ul> The solution: I identified the correct directory (learning_log/staticfiles) and removed duplicates.</ul>
<li>Incorrect BASE_DIR config</li>
<ul>base_dir was incorrectly set (BASE_DIR = Path(__file__).resolve().parent.parent.parent) and did not point to the correct directory. The correct config was (BASE_DIR = Path(__file__).resolve().parent)</ul>
<li>Errors with collectstatic</li>
<ul>Running python manage.py collectstatic produced errors because STATIC_ROOT was not set to a valid filesystem path. The solution was to move the static asset configuration outside of the conditional block for Heroku specific settings. This allowed the static asset config to be appied in both local and production environments. </ul>
<li>Heroku Deployment issues</li>
  <ul>The application continuously failed with 400 errors due to a misconfigured ALLOWED_HOST variable.</ul>
<li>Hard-coded Secret Key</li>
<ul> The textbook used a hardcoded key for development. To solve this, I created an environment variable to store the key. Did research to learn how to rotate secret keys for additional security. </ul>

# Security Features
<li>User Authentication and Authorization</li>
  <ul>	Restricted access to certain pages using the @login_required decorator. This code checks to see if a user is logged in and will only run the code if they are. </ul>
  <ul>I modified the Topic model by adding a foreign key relationship to a user. 
	check_topic_owner needs to accept Request & topic_id
	it retrieves the topic using topic_id
	then, an if loop checks if a topic owner is the user making the request. If they don’t match, raise a 404 exception. </ul>
 
<li>Password Hashing</li>
  <ul>Django uses built-in password hashing. </ul>
  
<li>Form Validation</li>
  <ul>Validated user inputs to prevent malicious or invalid data submissions using the is_valid() function </ul>
  
<li>CSRF Protection</li>
  <ul>CSRF tokens have been added to templates and forms. These tokens protect forms from cross-site request forgery attacks. </ul>
  
<li>URL Protection</li>
  <ul>Customized views to show only user-specific data and required the @login_required decorator</ul>


# Project Notes
## Naming Conventions
The naming convention is a little confusing
	startapp: will create 1 folder which contains all files associated to the application. 
		models.py
		admin.py
	startproject: will create these files
		settings.py
		urls.py
		wsgi.py
	these files help control how Django interacts with your system and manages your project. 


## in models.py :
__str__(self):
You need this to display the entries properly.

class Meta: 
	Needed to properly display correct grammar for multiple entries. 

Making the Home Page 
1. Project Folder
    1. update urls.py
2. App Folder
    1. create new urls.py
3. App Folder
    1. create folders
    2. create index.html file


## Django version 1.11 no longer uses the ‘login’ function. 
You instead need to use ‘LoginView’
This also changes the code: 
	Replace ‘login’ with:
		LoginView.as_view(template_name=‘users/login.html’)
	Remove the dictionary because the LoginView doesn’t accept this argument directly. Instead, you specify the template name directly with ‘as_view()” method call. 

<code>from django.urls import path
from django.contrib.auth.views import login

from . import views

app_name = ‘users’
urlpatterns = [
	# TEXTBOOK Login Page
	path(‘login/‘, login, {‘template_name’: ‘users/login.html’},
		name=‘login’),
	# NEW CODE
	path('login/', LoginView.as_view(template_name='users/login.html'), 
		name='login'),

]
</code>
