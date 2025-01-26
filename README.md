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
