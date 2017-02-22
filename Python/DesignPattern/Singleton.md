# 单例模式

```
class Singleton(object):
  def __new__(cls, *args, **kw):
    if not hasattr(cls, '_instant'):
      orig = Super(Singleton, cls)
      cls['_instant'] = orig.__new__(cls, *args, **kw)
    return cls['_instant']

class Myclass(Singleton):
  pass
```

```
def singleton(cls, *args, **kw):
  instances = {}
  def getinstant()
    if cls not in instants:
      instances[cls] = cls(*args, **kw)
    return instances[cls]
  return getinstant

@singleton
class Myclass(object):
  pass
```

```
# mysingleton.py
class My_Singleton(object):
  def foo(self):
    pass

mysingleton = new My_Singleton()

# to use
from mysingleton import mysingleton

mysingleton.foo()
```
