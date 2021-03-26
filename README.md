# testdriven.io-blog-modern-tdd-testdriven.io-blog-modern-tdd-Real-Application-blog_app

## Coverage

Now, with our application tested, it's the time to check code coverage. So let's install a pytest plugin for coverage called pytest-cov:

```bash
(venv) yusuke.sato@app-0001-dev ~/courses/testdriven.io/blog/modern-tdd/Real-Application/blog_app (main) 
$ pip install pytest-cov
```

After the plugin is installed, we can check code coverage of our blog application like this:

```python
(venv) yusuke.sato@app-0001-dev ~/courses/testdriven.io/blog/modern-tdd/Real-Application/blog_app (main) 
$ python -m pytest tests --cov=blog
=============================================================================================== test session starts ===============================================================================================
platform linux -- Python 3.8.6, pytest-6.2.2, py-1.10.0, pluggy-0.13.1
rootdir: /home/ys-office.me/yusuke.sato/courses/testdriven.io/blog/modern-tdd/Real-Application/blog_app/tests, configfile: pytest.ini
plugins: cov-2.11.1
collected 10 items                                                                                                                                                                                                

tests/test_article/test_app.py ......                                                                                                                                                                       [ 60%]
tests/test_article/test_commands.py ..                                                                                                                                                                      [ 80%]
tests/test_article/test_queries.py ..                                                                                                                                                                       [100%]

----------- coverage: platform linux, python 3.8.6-final-0 -----------
Name               Stmts   Miss  Cover
--------------------------------------
blog/__init__.py       0      0   100%
blog/app.py           25      1    96%
blog/commands.py      16      0   100%
blog/models.py        57      1    98%
blog/queries.py       12      0   100%
--------------------------------------
TOTAL                110      2    98%


=============================================================================================== 10 passed in 0.40s ================================================================================================
```

## End-to-end Tests

1. create a new article
2. list articles
3. get the first article from the list

First, install the [requests](https://requests.readthedocs.io/en/master/) library:

### Results

```python
(venv) yusuke.sato@app-0001-dev ~/courses/testdriven.io/blog/modern-tdd/Real-Application/blog_app (main) 
$ FLASK_APP=blog/app.py python -m flask run
 * Serving Flask app "blog/app.py"
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
127.0.0.1 - - [26/Mar/2021 09:17:28] "POST /create-article/ HTTP/1.1" 200 -
127.0.0.1 - - [26/Mar/2021 09:17:28] "GET /article-list/ HTTP/1.1" 200 -
127.0.0.1 - - [26/Mar/2021 09:17:28] "GET /article/f16fcfa3-b2f6-4b51-944d-27d44b70a16d/ HTTP/1.1" 200 -
```

```python
yusuke.sato@app-0001-dev ~/courses/testdriven.io/blog/modern-tdd/Real-Application/blog_app (main) 
$ python -m pytest tests -m 'e2e'
========================================= test session starts ==========================================
platform linux -- Python 3.8.6, pytest-6.2.2, py-1.10.0, pluggy-0.13.1
rootdir: /home/ys-office.me/yusuke.sato/courses/testdriven.io/blog/modern-tdd/Real-Application/blog_app/tests, configfile: pytest.ini
plugins: cov-2.11.1
collected 11 items / 10 deselected / 1 selected                                                        

tests/test_article/test_app.py .                                                                 [100%]

=================================== 1 passed, 10 deselected in 0.17s ===================================
```
