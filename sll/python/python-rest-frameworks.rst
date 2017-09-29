
FLASK VS DJANGO VS FALCON FOR REST API
======================================


Why I think Flask is for us:
I’ve done a lot of research and I’m going to say that I think Flask is the correct choice of web framework for our team at this point in time. I think for a number of reasons that it beats out Django/Pyramid long-term for what our use-cases will be, both API-wise and as a backend for a UI. We gain performance benefits over Django (according to many of the benchmarks people have done anyway, although I’d believe it regardless given how monolithic Django is), easy integration of Jinja2 templating, and easy integration of SQLAlchemy. Also, even though Flask _still_ hasn’t gone to version 1.0 after all this time, there is _finally_ a recent release of all the commits in master that had been accumulating, and it would seem Armin Ronacher (its author and a prominent member of the Python community) has transferred its main repo to a separate github org instead of his user to facilitate a faster release cycle and community contributions. And if we really want to, it would be very little work to still spin up a Django instance and throw together a handful of models for the admin even just as an interim FAB replacement. If at some point in the future performance becomes an issue we can look at rebuilding poorly performing portions in Falcon… but that’s a good ways in the future, using Falcon and properly securing it involves a *lot* of glue code and reinventing the wheel since what you gain in speed you lose in code that’s already written for you. Now, I _did_ turn up three or so restful toolkits for Flask, and since I’m not familiar with any of them, we’ll need to do some more research to find which one will be best for us:

Flask ReST toolkits:
http://python-eve.org/
http://flask-restful.readthedocs.io/en/0.3.5/
https://flask-restless.readthedocs.io/en/stable/

additional resources:
http://flask.pocoo.org/
http://wtforms.readthedocs.io/en/latest/index.html
https://flask-wtf.readthedocs.io/en/latest/
http://flask-limiter.readthedocs.io/en/stable/
https://damyanon.net/flask-series-security/
https://pythonhosted.org/Flask-Security/
https://github.com/maxcountryman/flask-login
https://github.com/lepture/flask-oauthlib
https://code.tutsplus.com/tutorials/flask-authentication-with-ldap--cms-23101
https://github.com/graup/flask-restless-security
https://pythonhosted.org/Flask-OAuth/ (depends on https://github.com/joestump/python-oauth2)
https://pythonhosted.org/Flask-Session/



http://python-guide-pt-br.readthedocs.io/en/latest/scenarios/web/
https://www.fullstackpython.com/api-creation.html

django:
+   django has faster up and running times due to batteries included
+   built-in form system with additional functionality from crispyforms
+   django-rest-framework provides a number of things such as
    > serialization
    > auth support
    > rate limiting
    > throttling
-   official but not terribly smooth support for sqlalchemy and jinja2

flask <http://flask.pocoo.org/>:
+   flask has smooth jinja2 support
+   good sqlalchemy integration
+   rate limiting via <http://flask-limiter.readthedocs.io/en/stable/>
|   form support through WTForms <http://wtforms.readthedocs.io/en/latest/index.html>
+   https://flask-wtf.readthedocs.io/en/latest/
-   insufficient built-in security measures

falcon:
+   fast as @#$%
-   absolutely bare-bones, have to implement everything yourself

pyramid <https://trypyramid.com/>:
http://pylonsproject.org/
http://docs.pylonsproject.org/projects/pyramid/en/latest/
?
https://github.com/uralbash/awesome-pyramid#restful-api
https://realpython.com/blog/python/create-a-rest-api-in-minutes-with-pyramid-and-ramses/

*   Building ReST APIs:
    - Django: django-rest-framework
    - Flask: http://python-eve.org/ or http://flask-restful.readthedocs.io/en/0.3.5/ or https://flask-restless.readthedocs.io/en/stable/
    - Pyramid: https://cornice.readthedocs.io/en/latest/
    - Falcon: https://github.com/timothycrosley/hug

1. Does flask easily support multiple login methods? (email + pass vs oauth etc)
https://damyanon.net/flask-series-security/
https://pythonhosted.org/Flask-Security/
https://github.com/maxcountryman/flask-login
https://github.com/lepture/flask-oauthlib
https://code.tutsplus.com/tutorials/flask-authentication-with-ldap--cms-23101
https://github.com/graup/flask-restless-security
https://pythonhosted.org/Flask-OAuth/ (depends on https://github.com/joestump/python-oauth2)
https://pythonhosted.org/Flask-Session/

2. How does it handle CSRF tokens?
http://wtforms.readthedocs.io/en/latest/index.html
https://flask-wtf.readthedocs.io/en/latest/

3. Does it inherently do proper escaping to help prevent XSS attacks?
jinja2
https://damyanon.net/flask-series-security/

4. I'm sure these can be manually set but does it happen to set X-Frame-Options, X-XSS-Protection, nosniff, HSTS headers by default?
set in middleware or nginx

5. How easy is it to ensure that all cookies (including session) are marked with httponly and secure?
http://flask.pocoo.org/docs/0.12/quickstart/#sessions ?


diff auth for different endpoints?

