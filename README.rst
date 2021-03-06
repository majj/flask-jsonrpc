Flask JSON-RPC
==============

A basic JSON-RPC implementation for your Flask-powered sites based on `django-json-rpc <https://github.com/samuraisam/django-json-rpc>`_.

Some reasons you might want to use:

* Simple, powerful, flexible and pythoic API.
* The Web browseable API.
* Support for authentication.
* Proxy to test your JSON Service.
* Run-time type checking.
* Extensive documentation, and great community support.

For support python 3.3 or later use the branch `py3k <https://github.com/cenobites/flask-jsonrpc/tree/py3k>`_ (experimental).

There is a live example API for testing purposes, `available here <http://flask-jsonrpc.herokuapp.com/api/browse>`_.

**Below:** *Screenshot from the browsable API*

.. image:: https://f.cloud.github.com/assets/298350/1575590/203c595a-5150-11e3-99a0-4a6fd9bcbe52.png

Adding Flask JSON-RPC to your application
*****************************************

1. Installation

::

    $ pip install Flask-JSONRPC

or

::

    $ git clone git://github.com/cenobites/flask-jsonrpc.git
    $ cd flask-jsonrpc
    $ python setup.py install


2. Getting Started

Create your application and initialize the Flask-JSONRPC.

::

    from flask import Flask
    from flask_jsonrpc import JSONRPC

    app = Flask(__name__)
    jsonrpc = JSONRPC(app, '/api')

Write JSON-RPC methods.

::

    @jsonrpc.method('App.index')
    def index():
        return 'Welcome to Flask JSON-RPC'

All code of Example `run.py <https://github.com/cenobites/flask-jsonrpc/blob/master/run.py>`_.


3. Running

::
    
    $ python run.py
     * Running on http://0.0.0.0:5000/
     

4. Testing

::

    $ curl -i -X POST -d '{"jsonrpc": "2.0", "method": "App.index", "params": {}, "id": "1"}' http://localhost:5000/api
    HTTP/1.0 200 OK
    Content-Type: application/json
    Content-Length: 77
    Server: Werkzeug/0.8.3 Python/2.7.3
    Date: Fri, 14 Dec 2012 19:26:56 GMT
    
    {
      "jsonrpc": "2.0",
      "id": "1",
      "result": "Welcome to Flask JSON-RPC"
    }


Testing your service
********************

You can test your service using the provided web browsable API, available at http://localhost:5000/api/browse (if using the url patterns from above) or with the included ServiceProxy:

::

    >>> from flask_jsonrpc.proxy import ServiceProxy
    >>> server = ServiceProxy('http://localhost:5000/api')
    >>>
    >>> server.App.index()
    {'jsonrpc': '2.0', 'id': '91bce374-462f-11e2-af55-f0bf97588c3b', 'result': 'Welcome to Flask JSON-RPC'}

We add the ``jsonrpc_version`` variable to the request object. It be either '1.0', '1.1' or '2.0'. Arg.

For more tests see `Examples <https://github.com/cenobites/flask-jsonrpc/wiki/Examples>`_.

Dependecies
***********

* Python (2.6.5+), (2.7, 3.2, 3.3) or later (http://www.python.org)
* Flask 0.9 or later (http://flask.pocoo.org)


Project Information
*******************

:Author: Cenobit Technologies, Inc.
:Version: v0.0.1 of 2012/12/14
:License: `New BSD License <http://opensource.org/licenses/BSD-3-Clause>`_
