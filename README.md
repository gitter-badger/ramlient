# ramlient - RAML client for python
> RESTful API Modeling Language (RAML) client

***

[![PyPI License](https://img.shields.io/pypi/l/ramlient.svg)](https://github.com/timofurrer/ramlient/blob/master/LICENSE)
[![Build Status](https://travis-ci.org/timofurrer/ramlient.svg?branch=master)](https://travis-ci.org/timofurrer/ramlient)
<br>
[![codecov.io](https://codecov.io/github/timofurrer/ramlient/coverage.svg?branch=master)](https://codecov.io/github/timofurrer/ramlient?branch=master)
[![Code Health](https://landscape.io/github/timofurrer/ramlient/master/landscape.svg?style=flat)](https://landscape.io/github/timofurrer/ramlient/master)
[![Code Issues](https://www.quantifiedcode.com/api/v1/project/5746a7109123441bbd833013b5f173c5/badge.svg)](https://www.quantifiedcode.com/app/project/5746a7109123441bbd833013b5f173c5)
<br>
[![PyPI version](https://badge.fury.io/py/ramlient.svg)](https://badge.fury.io/py/ramlient)
[![PyPI](https://img.shields.io/pypi/pyversions/ramlient.svg)](https://pypi.python.org/pypi/ramlient)
[![PyPI](https://img.shields.io/pypi/wheel/ramlient.svg)](https://pypi.python.org/pypi/ramlient)
[![PyPI](https://img.shields.io/pypi/dm/ramlient.svg)](https://pypi.python.org/pypi/ramlient)

Author: Timo Furrer <tuxtimo@gmail.com> <br>
License: **MIT** <br>

***

**ramlient** makes it very easy to access RAML based APIs. Kenneth would probably call it *raml for humans* or something ;)

## Installation

Use pip to install `ramlient`:

```bash
pip install ramlient
```

## Usage

Let's assume you have the following simple RAML file:

```raml
#%RAML 0.8
---
title: Example API
baseUri: http://example.com
securitySchemes:
  - basic:
      type: Basic Authentication
/resource:
  displayName: First One
  put:
    responses:
      200:
      201:
      203:
  get:
    description: get the first one
    headers:
      x-custom:
    responses:
      200:
  /{resourceId}:
    description: This is a resource description *with* some _markdown_ embedded in it
    uriParameters:
      resourceId:
        required: true
        description: Which resoure would you like to view
    get:
      queryParameters:
        filter:
          description: What to filter
          type: string
      responses:
        200:
```

Use `ramlient` to make easy requests to the routes:

```python
from ramlient import Client

client = Client("api.raml")
response = client.resource.get()
resource = client.resource.resourceId(1).get()
```
