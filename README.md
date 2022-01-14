[Bubble.io]: https://bubble.io/

Bubble-Client
=============

[![PyPI](https://img.shields.io/pypi/v/bubble-client.svg)](https://pypi.org/project/bubble-client)
[![License](https://img.shields.io/github/license/Refty/bubble-client)](LICENSE)
[![Code style](https://img.shields.io/badge/code%20style-black-black)](https://github.com/ambv/black)

Python client for the [Bubble.io][] APIs

Installation
------------

```shell
pip install bubble-client
```

Examples
--------

* Get users (or any Bubble thing, really):

```python
>>> from bubble_client import configure, BubbleThing
>>> configure(base_url=..., token=...)

>>> class User(BubbleThing):
...     pass

>>> async for user in User.get():
...     print(user)
User({'name': 'Dr. Jekyll', ...})
User({'name': 'Mr. Hyde', ...})

>>> user.name
'Mr. Hyde'
```

* Join stuff!

```python
>>> class Pet(BubbleThing):
...     pass

>>> pet = await pet.get_one()
>>> await pet.join("created_by", User)

>>> pet.type
'dog'
>>> pet.created_by
User({'name': 'Mr. Hyde', ...})
>>> pet.created_by.name
'Mr. Hyde'
```

* Also works on cursors!

```python
>>> async for pet in Pet.get().join("created_by", User):
...     print(pet)
Pet({'type': 'dog', 'created_by': User({'name': 'Dr. Jekyll', ...}), ...})
Pet({'type': 'donkey', 'created_by': User({'name': 'Dr. Jekyll', ...}), ...})
```
