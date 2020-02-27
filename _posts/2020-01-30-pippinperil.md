---
layout: post
title: Perils of Pip Pinning in Production
tags:  python pip version semver dependency
---

# work in progress

# just pip freeze it, bro

Tell me if this sounds familiar. You have your python project, and you want to make
it ready for production/deployment/tech transfer. It's been sitting on your system
for a few months and now you have to get your 
coworker/devops/that-one-dude-obsessed-with-docker to build your project, reliably 
from scratch. You say, I know, I'll just `pip freeze > requirements.txt` and then
the install script can just `pip install -r requirements.txt` and you're golden!
Right?

What could *possibly* go wrong?

Well, you'll likely be able to restore that state exactly. Exact same python, 
exact same packages. 

# overconstrained

The first problem is the way pip freeze expresses its state. Your pip freeze 
looks something like this:

```.env
absl-py==0.9.0
attrs==19.3.0
...
urllib3==1.25.7
Werkzeug==0.16.0
wrapt==1.10.11
``` 

It lists every single dependency, however important or unimportant, pinned to the 
most minute version. 

# -e flags
```python


```