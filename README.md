
# `connection-uri` [![PyPI version](https://badge.fury.io/py/connection-uri.svg)](https://badge.fury.io/py/connection-uri) [![Build Status](https://travis-ci.com/grimen/python-connection-uri.svg?branch=master)](https://travis-ci.com/grimen/python-connection-uri) [![Coverage Status](https://codecov.io/gh/grimen/python-connection-uri/branch/master/graph/badge.svg)](https://codecov.io/gh/grimen/python-connection-uri)

*A robust connection URI parser/stringifier - for Python.*

## Introduction

This connection URI library was implemented in lack of robust Python alternatives. This one supports absolute/relative multi-host connection URIs with smart fallbacks.


## Install

Install using **pip**:

```sh
$ pip install connection-uri
```


## Use

Very basic **[example](https://github.com/grimen/python-connection-uri/tree/master/examples/basic.py)**:

```python
import connection_uri

basic_connection_uri = 'localhost:3000/namespace/foo/'
basic_connection_options = connection_uri.unpack(basic_connection_uri)

print('\nconnection_uri.unpack({0})\n\n{1}\n'.format(basic_connection_uri, basic_connection_options))
#
# {
#     'protocol': 'http',
#     'auth': None,
#
#     'endpoint': 'localhost:3000',
#     'endpoints': ['localhost:3000'],
#
#     'host': 'localhost',
#     'hosts': ['localhost'],
#
#     'port': 3000,
#     'ports': [3000],

#     'path': '/namespace/foo/',
#     'query': {},
#
#     'credentials': {
#         'username': None,
#         'password': None,
#     },
#     'key': 'namespace/foo',
#     'namespace': 'namespace/foo',
#
#     'url': 'http://localhost:3000/namespace/foo/',
#     'urls': [
#         'http://localhost:3000/namespace/foo/'
#     ],
# }
#

basic_connection_uri = connection_uri.pack(basic_connection_options)

print('\nconnection_uri.pack({0})\n\n{1}\n'.format(basic_connection_options, basic_connection_uri))
#
# 'http://localhost:3000/namespace/foo/'
#

print('---')

complex_multihost_uri = 'foo://m+4.gTe~5e^(:m+4.gTe~5e^(@ds143144-a0.mlab.com:43144,ds143144-a1.mlab.com:43145/bar-baz'
complex_multihost_options = connection_uri.unpack(complex_multihost_uri)

print('\nconnection_uri.unpack({0})\n\n{1}\n'.format(complex_multihost_uri, complex_multihost_options))
#
# {
#     'protocol': 'foo',
#     'auth': 'm+4.gTe~5e^(:m+4.gTe~5e^(',
#
#     'host': 'ds143144-a0.mlab.com',
#     'port': 43144,
#
#     'endpoint': 'ds143144-a0.mlab.com:43144',
#     'endpoints': ['ds143144-a0.mlab.com:43144', 'ds143144-a1.mlab.com:43145'],
#
#     'host': 'ds143144-a0.mlab.com',
#     'hosts': ['ds143144-a0.mlab.com', 'ds143144-a1.mlab.com'],
#
#     'port': 43144,
#     'ports': [43144, 43145],
#
#     'path': '/bar-baz',
#     'query': {},
#
#     'credentials': {
#         'username': 'm+4.gTe~5e^(',
#         'password': 'm+4.gTe~5e^(',
#     },
#     'key': 'bar-baz',
#     'namespace': 'bar-baz',
#
#     'url': 'foo://m+4.gTe~5e^(:m+4.gTe~5e^(@ds143144-a0.mlab.com:43144,ds143144-a1.mlab.com:43145/bar-baz',
#     'urls': [
#         'foo://m+4.gTe~5e^(:m+4.gTe~5e^(@ds143144-a0.mlab.com:43144/bar-baz',
#         'foo://m+4.gTe~5e^(:m+4.gTe~5e^(@ds143144-a1.mlab.com:43145/bar-baz'
#     ],
# }
#

complex_multihost_uri = connection_uri.pack(complex_multihost_options)

print('\nconnection_uri.pack({0})\n\n{1}\n'.format(complex_multihost_options, complex_multihost_uri))
#
# 'foo://m+4.gTe~5e^(:m+4.gTe~5e^(@ds143144-a0.mlab.com:43144,ds143144-a1.mlab.com:43145/bar-baz'
#

# NOTE: see tests for more advanced examples, e.g. the library handles absolute and relative URIs, etc.

```


## Test

Clone down source code:

```sh
$ make install
```

Run **colorful tests**, with only native environment (dependency sandboxing up to you):

```sh
$ make test
```

Run **less colorful tests**, with **multi-environment** (using **tox**):

```sh
$ make test-tox
```


## About

This project was mainly initiated - in lack of solid existing alternatives - to be used at our work at **[Markable.ai](https://markable.ai)** to have common code conventions between various programming environments where **Python** (research, CV, AI) is heavily used.


## License

Released under the MIT license.
