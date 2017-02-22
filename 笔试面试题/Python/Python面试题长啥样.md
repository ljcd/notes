> 参考：Python面试题长啥样？[面试题整理]（作者：路人甲）：https://zhuanlan.zhihu.com/p/21856569?refer=passer

1. How are arguments passed – by reference of by value?  
  [is-python-callbyvalue-or-callbyreference-neither](https://jeffknupp.com/blog/2012/11/13/is-python-callbyvalue-or-callbyreference-neither/)

2. Do you know what list and dict comprehensions are? Can you give an example?
  > List comprehensions provide a concise way to create lists.

  > You can use dict comprehensions in ways very similar to list comprehensions,
  except that they produce Python dictionary objects instead of list objects.

  ` squares = [x**2 for x in range(10)] `

  ```
  >>> print {i : chr(65+i) for i in range(4)}
      {0 : 'A', 1 : 'B', 2 : 'C', 3 : 'D'}
  ```

  ` {k : v for k, v in someDict.iteritems()} `

  [list-comprehensions](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions)

  [dict-comprehensions](https://www.python.org/dev/peps/pep-0274/)

3. What is PEP 8?

  > PEP 8 is the style guide for Python code.

  [PEP 8](https://www.python.org/dev/peps/pep-0008/)

4. Do you use virtual environments?

  > virtualenv is a tool to create isolated Python environments.

  [virtualenv](https://virtualenv.pypa.io/en/stable/)

5. Can you sum all of the elements in the list, how about to multuply them and get the result?

  ` reduce(lambda x, y: x+y, a_list) `  
  ` reduce(lambda x, y: x*y, a_list) `

6. Do you know what is the difference between lists and tuples? Can you give me an example for their usage?

  > Apart from tuples being immutable there is also a semantic distinction that
  should guide their usage. Tuples are heterogeneous data structures (i.e., their
  entries have different meanings), while lists are homogeneous sequences.
  Tuples have structure, lists have order.

  ```
  someTuple = (1,2)
  someList  = [1,2]
  ```

  [whats-the-difference-between-list-and-tuples](http://stackoverflow.com/questions/626759/whats-the-difference-between-list-and-tuples)

7. Do you know the difference between range and xrange?

  > range creates a list, so if you do range(1, 10000000) it creates a list in
  memory with 9999999 elements.
  xrange is a sequence object that evaluates lazily.

  [What is the difference between range and xrange functions in Python 2.X?](http://stackoverflow.com/questions/94935/what-is-the-difference-between-range-and-xrange-functions-in-python-2-x)

8. Tell me a few differences between Python 2.x and 3.x
  1. The __future__ module
    > Python 3.x introduced some Python 2-incompatible keywords and features that
     can be imported via the in-built __future__ module in Python 2.

    `from __future__ import division`

  2. The print function

    > Python 2’s print statement has been replaced by the print() function, meaning
    that we have to wrap the object that we want to print in parantheses. Python 2
    doesn’t have a problem with additional parantheses, but in contrast, Python 3
    would raise a SyntaxError if we called the print function the Python 2-way
    without the parentheses.

  3. Integer division

    3/2，在 Python 2.x 中得到 1，在 Python 3.x 中得到 1.5

  4. Unicode

    > The main difference between Python 2 and Python 3 is the basic types that
    exist to deal with texts and bytes. On Python 3 we have one text type: str
    which holds Unicode data and two byte types bytes and bytearray.

    > On the other hand on Python 2 we have two text types: str which for all
    intents and purposes is limited to ASCII + some undefined data above the 7
    bit range, unicode which is equivalent to the Python 3 str type and one byte
    type bytearray which it inherited from Python 3.

  5. xrange

    > In Python 3, the range() was implemented like the xrange() function so
    that a dedicated xrange() function does not exist anymore (xrange() raises
    a NameError in Python 3).

  6. Raising exceptions

    > Where Python 2 accepts both notations, the ‘old’ and the ‘new’ syntax,
    Python 3 chokes (and raises a SyntaxError in turn) if we don’t enclose the
    exception argument in parentheses

    ```
    Python 2.7.6
    raise IOError, "file error"
    raise IOError("file error")
    ```

    ```
    Python 3.4.1
    raise IOError, "file error"  # SyntaxError: invalid syntax
    raise IOError("file error")
    ```

  7. Handling exceptions

    > In Python 3 we have to use the “as” keyword when handling exceptions.

    ```
    Python 2

    try:
        let_us_cause_a_NameError
    except NameError, err:
        print err, '--> our error message'
    ```

    ```
    Python 3

    try:
        let_us_cause_a_NameError
    except NameError as err:
        print(err, '--> our error message')
    ```

  8. The next() function and .next() method

    You can use next() and .next() in Python 2.7.5 and use next() in Python 3,
    but can't use .next() in Python 3(calling the .next() method raises an
    AttributeError).

    ```
    Python 2

    my_generator = (letter for letter in 'abcdefg')
    next(my_generator)   # got 'a'
    my_generator.next()  # got 'b'
    ```

    ```
    Python 3

    my_generator = (letter for letter in 'abcdefg')
    next(my_generator)   # got 'a'
    my_generator.next()  # AttributeError
    ```

  9. For-loop variables and the global namespace leak

    > In Python 3.x for-loop variables don’t leak into the global namespace anymore!

    ```
    Python 2

    i = 1
    print 'before: i =', i
    print 'comprehension: ', [i for i in range(5)]
    print 'after: i =', i

    before: i = 1
    comprehension:  [0, 1, 2, 3, 4]
    after: i = 4
    ```

    ```
    Python 3

    i = 1
    print 'before: i =', i
    print 'comprehension: ', [i for i in range(5)]
    print 'after: i =', i

    before: i = 1
    comprehension: [0, 1, 2, 3, 4]
    after: i = 1
    ```

  10. Comparing unorderable types

    > Another nice change in Python 3 is that a TypeError is raised as warning
    if we try to compare unorderable types.

    ```
    Python 2

    print [1, 2] > 'foo'   # False
    print (1, 2) > 'foo'   # True
    print [1, 2] > (1, 2)  # False
    ```

    ```
    Python 3

    print([1, 2] > 'foo')   # TypeError: unorderable types: list() > str()
    print((1, 2) > 'foo')   #
    print([1, 2] > (1, 2))  #
    ```

  11. Parsing user inputs via input()

    > Fortunately, the input() function was fixed in Python 3 so that it always
    stores the user inputs as str objects. In order to avoid the dangerous
    behavior in Python 2 to read in other types than strings, we have to use
    raw_input() instead.

    ```
    Python 2

    >>> my_input = input('enter a number: ')

    enter a number: 123

    >>> type(my_input)
    <type 'int'>

    >>> my_input = raw_input('enter a number: ')

    enter a number: 123

    >>> type(my_input)
    <type 'str'>
    ```

    ```
    Python 3

    >>> my_input = input('enter a number: ')

    enter a number: 123

    >>> type(my_input)
    <class 'str'>
    ```

  12. Returning iterable objects instead of lists

    > Some functions and methods return iterable objects in Python 3 now,  
     instead of lists in Python 2. And for those cases where we really need the
     list-objects, we can simply convert the iterable object into a list via
     the list() function.

    ```
    Python 2

    print range(3)              # [0, 1, 2]
    print type(range(3))        # <type 'list'>
    ```

    ```
    Python 3

    print(range(3))             # range(0, 3)
    print(type(range(3)))       # <class 'range'>
    print(list(range(3)))       # [0, 1, 2]
    ```

    > Some more commonly used functions and methods that don’t return lists
    anymore in Python 3: zip(), map(), filter(), dictionary’s .keys() method,
    dictionary’s .values() method, dictionary’s .items() method

  13. Banker’s Rounding

    > Python 3 adopted the now standard way of rounding decimals when it results
    in a tie (.5) at the last significant digits. Now, in Python 3, decimals are
     rounded to the next even number.

    ```
    Python 2

    round(15.5)  # 16.0
    round(16.5)  # 17.0
    ```

    ```
    Python 3

    round(15.5)  # 16
    round(16.5)  # 16
    ```

  [The key differences between Python 2.7.x and Python 3.x with examples](http://sebastianraschka.com/Articles/2014_python_2_3_key_diff.html)

  [More About Unicode in Python 2 and 3](http://lucumr.pocoo.org/2014/1/5/unicode-in-2-and-3/)

9. What are decorators and what is their usage?

  > A decorator is the name used for a software design pattern. Decorators
  dynamically alter the functionality of a function, method, or class without
  having to directly use subclasses or change the source code of the function
  being decorated.
  A Python decorator is a specific change to the Python syntax that allows us
  to more conveniently alter functions and methods (and possibly classes in a
  future version).  

  [PythonDecorators](https://wiki.python.org/moin/PythonDecorators)
  [How to make a chain of function decorators in Python?](https://stackoverflow.com/questions/739654/how-to-make-a-chain-of-function-decorators-in-python)

10. The with statement and its usage.

  [Understanding Python's "with" statement](http://effbot.org/zone/python-with-statement.htm)

11. 说说你对 zen of python 的理解，你有什么办法看到它。

  在 Python 命令行中输入 import this 即可看到。

  > Beautiful is better than ugly.
  Explicit is better than implicit.
  Simple is better than complex.
  Complex is better than complicated.
  Flat is better than nested.
  Sparse is better than dense.
  Readability counts.
  Special cases aren't special enough to break the rules.
  Although practicality beats purity.
  Errors should never pass silently.
  Unless explicitly silenced.
  In the face of ambiguity, refuse the temptation to guess.
  There should be one-- and preferably only one --obvious way to do it.
  Although that way may not be obvious at first unless you're Dutch.
  Now is better than never.
  Although never is often better than *right* now.
  If the implementation is hard to explain, it's a bad idea.
  If the implementation is easy to explain, it may be a good idea.
  Namespaces are one honking great idea -- let's do more of those!

  > 优美胜于丑陋（Python 以编写优美的代码为目标）
  明了胜于晦涩（优美的代码应当是明了的，命名规范，风格相似）
  简洁胜于复杂（优美的代码应当是简洁的，不要有复杂的内部实现）
  复杂胜于凌乱（如果复杂不可避免，那代码间也不能有难懂的关系，要保持接口简洁）
  扁平胜于嵌套（优美的代码应当是扁平的，不能有太多的嵌套）
  间隔胜于紧凑（优美的代码有适当的间隔，不要奢望一行代码解决问题）
  可读性很重要（优美的代码是可读的）
  即便假借特例的实用性之名，也不可违背这些规则（这些规则至高无上）
  不要包容所有错误，除非你确定需要这样做（精准地捕获异常，不写 except:pass 风格的代码）
  当存在多种可能，不要尝试去猜测
  而是尽量找一种，最好是唯一一种明显的解决方案（如果不确定，就用穷举法）
  虽然这并不容易，因为你不是 Python 之父（这里的 Dutch 是指 Guido ）
  做也许好过不做，但不假思索就动手还不如不做（动手之前要细思量）
  如果你无法向人描述你的方案，那肯定不是一个好方案；反之亦然（方案测评标准）
  命名空间是一种绝妙的理念，我们应当多加利用（倡导与号召）

  [Python 之禅的翻译和解释](http://blog.csdn.net/gzlaiyonghao/article/details/2151918)

12. github 上都 fork 过哪些 python 库，列举一下你经常使用的，每个库用一句话描述下其功能

13. 你调试 python 代码的方法有哪些？

  [调试-廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/00138683229901532c40b749184441dbd428d2e0f8aa50e000)
  [我常用的 Python 调试工具-伯乐在线](http://blog.jobbole.com/51062/)

14. 什么是 GIL(Global Interpreter Lock，全局解释器锁)

  > In CPython, the global interpreter lock, or GIL, is a mutex that prevents
  multiple native threads from executing Python bytecodes at once. This lock is
  necessary mainly because CPython’s memory management is not thread-safe.
  (However, since the GIL exists, other features have grown to depend on the
  guarantees that it enforces.)

  [Python的GIL是什么鬼，多线程性能究竟如何](http://cenalulu.github.io/python/gil-in-python/)

15. 什么是元类(meta_class)。

  > A metaclass is the class of a class. Like a class defines how an instance
  of the class behaves, a metaclass defines how a class behaves. A class is an
  instance of a metaclass.

  [What is a metaclass in Python?](http://stackoverflow.com/questions/100003/what-is-a-metaclass-in-python)

16. 对比一下 dict 中 items 与 iteritems。

  [What is the difference between dict.items() and dict.iteritems()?](http://stackoverflow.com/questions/10458437/what-is-the-difference-between-dict-items-and-dict-iteritems)

17. 是否遇到过 python 的模块间循环引用的问题，如何避免它？

  [The 10 Most Common Mistakes That Python Developers Make](https://www.toptal.com/python/top-10-mistakes-that-python-programmers-make)

18. 有用过 with statement 吗？它的好处是什么？

19. 说说 decorator 的用法和它的应用场景，如果可以的话，写一个 decorator。

  ```
  from functools import wraps
  from flask import make_response

  def allow_cross_domain(fun):
      @wraps(fun)
      def wrapper_fun(*args, **kwargs):
          rst = make_response(fun(*args, **kwargs))
          rst.headers['Access-Control-Allow-Origin'] = '*'
          rst.headers['Access-Control-Allow-Methods'] = 'PUT,GET,POST,DELETE'
          allow_headers = "Referer,Accept,Origin,User-Agent"
          rst.headers['Access-Control-Allow-Headers'] = allow_headers
          return rst
      return wrapper_fun

  @app.route('/hosts/')
  @allow_cross_domain
  def domains():
      pass
  ```

20. inspect 模块有什么用

  > The inspect module provides several useful functions to help get information about live objects such as modules, classes, methods, functions, tracebacks, frame objects, and code objects. For example, it can help you examine the contents of a class, retrieve the source code of a method, extract and format the argument list for a function, or get all the information you need to display a detailed traceback.
  There are four main kinds of services provided by this module: type checking, getting source code, inspecting classes and functions, and examining the interpreter stack.

  [inspect-Inspect live objects](https://docs.python.org/2/library/inspect.html)

21. 写一个类，并让它尽可能多的支持操作符

  ```
  class Book:
    title = ''
    pages = 0

    def __init__(self, title='', pages=0):
        self.title = title
        self.pages = pages

    def __add__(self, other):
        """Control adding two Books together or a Book and a number"""
        return int(self) + other

    def __radd__(self, other):
        """Control adding a Book and a number w/ the number first"""
        return int(self) + other

    def __int__(self):
        """Return the number of pages"""
        return self.pages

    def __str__(self):
        """Return the Book title"""
        return self.title

    def __lt__(self, other):
        """Return whether this book's page count is less than another number"""
        return self.pages < other

    def __le__(self, other):
        """Return whether this book's page count is less than or
        equal to another Book or a number
        """
        if isinstance(other, Book):
            return self.pages <= other.pages
        elif isinstance(other, (int, float)):
            return self.pages <= other
        else:
            return NotImplemented

    def __eq__(self, other):
        """Return whether this book's page count is equal to another number"""
        return self.pages == other

    def __ne__(self, other):
        """Return whether this book's page count is not equal to another number"""
        return self.pages != other

    def __gt__(self, other):
        """Return whether this book's page count is greater than another number"""
        return self.pages > other

    def __ge__(self, other):
        """Return whether this book's page count is greater than or
        equal to another Book or a number
        """
        if isinstance(other, Book):
            return self.pages >= other.pages
        elif isinstance(other, (int, float)):
            return self.pages >= other
        else:
            return NotImplemented
  ```

  [Operator Overloading in Python](http://blog.teamtreehouse.com/operator-overloading-python)
  [Data model - Python doc](https://docs.python.org/3/reference/datamodel.html#special-method-names)

22. 说一说你见过比较 cool 的 Python 实现。

23. Python 下多线程的限制以及多进程中传递参数的方式。

  CPython 是大部分环境下默认的 Python 执行环境，CPython 中存在全局解释锁（GIL），会导致
  Python 的多线程效率低下。
  多进程中传递参数的方式包括 pipe 和 queue。

  [多进程-廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/0013868323401155ceb3db1e2044f80b974b469eb06cb43000)
  [Python标准库08 多线程与同步 (threading包)](http://www.cnblogs.com/vamei/archive/2012/10/11/2720042.html)
  [Python标准库10 多进程初步 (multiprocessing包)](http://www.cnblogs.com/vamei/archive/2012/10/12/2721484.html)

24. Python是如何进行内存管理的？

25. 什么是 lambda 函数？它有什么好处?

  > Small anonymous functions can be created with the lambda keyword. This
  function returns the sum of its two arguments: `lambda a, b: a+b`. Lambda
  functions can be used wherever function objects are required. They are
  syntactically restricted to a single expression. Semantically, they are just
  syntactic sugar for a normal function definition.

  [Lambda Expression](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions)

26. 如何用 Python 输出一个 Fibonacci 数列？

  ```
  def F():
    a,b = 0,1
    yield a
    yield b
    while True:
        a, b = b, a + b
        yield b

  f = F()
  for i in xrange(10):
    print f.next()
  ```

27. 介绍一下 Python 中 webbrowser 的用法？

  > The webbrowser module provides a high-level interface to allow displaying
  Web-based documents to users.

  ```
  # 最常用的 open 函数
  webbrowser.open("http://www.baidu.com")
  ```

  [webbrowser — Convenient Web-browser controller](https://docs.python.org/2/library/webbrowser.html)
  [Python:使用浏览器打开网页](http://gohom.win/2015/12/22/pyWebbrowser/)

28. 解释一下 Python 的 and-or 语法。

  > and-or主要是用来模仿三目运算符 `bool ? a : b` 的，即当表达式 bool 为真，则取 a，否则取 b。
  and-or 技巧：bool and a or b 表达式，当 a 在布尔上下文中的值为假时，不会像 C 语言表达式
  `bool ? a : b` 那样工作。所以应该像这样安全地使用 and-or ：`(bool and [a] or [b])[0]`
  由于 [a] 是一个非空列表，所以它决不会为假。即使 a 是 0 或者 '' 或者其它假值，列表 [a] 也
  为真，因为它有一个元素。

  [深入Python(3): and、or以及and-or](http://www.cnblogs.com/BeginMan/p/3197123.html)

29. Python 是如何进行类型转换的？

  ```
  int(x)             将x转换为一个整数
  float(x)           将x转换到一个浮点数
  str(x)             将对象 x 转换为字符串
  tuple(s)           将序列 s 转换为一个元组
  list(s)            将序列 s 转换为一个列表
  set(s)             将序列 s 转换为一个集合
  ```

30. Python 如何实现单例模式？其他23种设计模式 Python 如何实现？

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

31. 如何用 Python 来进行查询和替换一个文本字符串？

    > str.replace(old, new[, count])
      Return a copy of the string with all occurrences of substring old
      replaced by new. If the optional argument count is given, only the first
      count occurrences are replaced.

    > re.sub(pattern, repl, string, count=0, flags=0)

    [re.sub](https://docs.python.org/2/library/re.html?highlight=re.sub#re.sub)

32. 如何用 Python 来发送邮件？

33. 有没有一个工具可以帮助查找 Python 的 bug 和进行静态的代码分析？

34. 有两个序列 a,b，大小都为 n，序列元素的值任意整形数，无序；
    要求：通过交换 a,b 中的元素，使[序列a元素的和]与[序列b元素的和]之间的差最小。

35. 如何用 Python 删除一个文件？

  > `os.remove(path)`
  Remove (delete) the file path. If path is a directory, OSError is raised; see
  rmdir() below to remove a directory. This is identical to the unlink()
  function documented below. On Windows, attempting to remove a file that is in
  use causes an exception to be raised; on Unix, the directory entry is removed
  but the storage allocated to the file is not made available until the
  original file is no longer in use.
  Availability: Unix, Windows.

  [os.remove(path)](https://docs.python.org/2/library/os.html?highlight=remove#os.remove)

36. Python如何 copy 一个文件？

  > `shutil.copyfile(src, dst)`
  Copy the contents (no metadata) of the file named src to a file named dst.
  dst must be the complete target file name; look at shutil.copy() for a copy
  that accepts a target directory path. If src and dst are the same files,
  Error is raised. The destination location must be writable; otherwise, an
  IOError exception will be raised. If dst already exists, it will be replaced.
  Special files such as character or block devices and pipes cannot be copied
  with this function. src and dst are path names given as strings.

  [shutil.copyfile](https://docs.python.org/2/library/shutil.html?highlight=copyfile#shutil.copyfile)

37. Python 程序中文输出问题怎么解决？

38. Python 代码得到列表 list 的交集与差集。

  > ^ 是按位异或操作符，相同为 0，相异为 1。

  ```
  a_list, b_list = [1, 2, 3, 4], [1, 4, 5]

  # 差集
  ret_list = list( set(a_list)^set(b_list) )

  # 并集
  ret_list = list( set(a_list).union(set(b_list)) )

  # 交集
  ret_list = list( set(a_list).union(set(b_list)) ^ (set(a_list)^set(b_list)) )
  ```

39. 写一个简单的 python socket 编程。

  [Python 的 Socket 编程教程](https://www.oschina.net/question/12_76126)

  ```
  # server

  import socket
  import sys
  from thread import *

  HOST = ''   # Symbolic name meaning all available interfaces
  PORT = 8888 # Arbitrary non-privileged port

  s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
  print 'Socket created'

  # Bind socket to local host and port
  try:
      s.bind((HOST, PORT))
  except socket.error , msg:
      print 'Bind failed. Error Code : ' + str(msg[0]) + ' Message ' + msg[1]
      sys.exit()

  print 'Socket bind complete'

  # Start listening on socket
  s.listen(10)
  print 'Socket now listening'

  # Function for handling connections. This will be used to create threads
  def clientthread(conn):
      # Sending message to connected client
      conn.send('Welcome to the server. Type something and hit enter\n') # send only takes string

      # infinite loop so that function do not terminate and thread do not end.
      while True:

          # Receiving from client
          data = conn.recv(1024)
          reply = 'OK...' + data
          if not data:
              break

          conn.sendall(reply)

      # came out of loop
      conn.close()

  # now keep talking with the client
  while 1:
      # wait to accept a connection - blocking call
      conn, addr = s.accept()
      print 'Connected with ' + addr[0] + ':' + str(addr[1])

      # start new thread takes 1st argument as a function name to be run, second is the tuple of arguments to the function.
      start_new_thread(clientthread ,(conn,))

  s.close()
  ```

  ```
  # client

  import socket   #for sockets
  import sys  #for exit

  # create an INET, STREAMing socket
  try:
      s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
  except socket.error:
      print 'Failed to create socket'
      sys.exit()

  print 'Socket Created'

  host = 'oschina.net';
  port = 80;

  try:
      remote_ip = socket.gethostbyname( host )

  except socket.gaierror:
      # could not resolve
      print 'Hostname could not be resolved. Exiting'
      sys.exit()

  # Connect to remote server
  s.connect((remote_ip , port))

  print 'Socket Connected to ' + host + ' on ip ' + remote_ip

  # Send some data to remote server
  message = "GET / HTTP/1.1\r\nHost: oschina.net\r\n\r\n"

  try :
      # Set the whole string
      s.sendall(message)
  except socket.error:
      # Send failed
      print 'Send failed'
      sys.exit()

  print 'Message send successfully'

  # Now receive data
  reply = s.recv(4096)

  print reply
  ```

40. Python 如何捕获异常。

41. 在Python中, list, tuple, dict, set有什么区别, 主要应用在什么样的场景?

42. 静态函数, 类函数, 成员函数的区别?

43. a=1, b=2, 不用中间变量交换a和b的值

44. 写一个函数, 输入一个字符串, 返回倒序排列的结果: 如: string_reverse(‘abcdef’), 返回: ‘fedcba’

45. 请用自己的算法, 按升序合并如下两个list, 并去除重复的元素:
  list1 = [2, 3, 8, 4, 9, 5, 6]
  list2 = [5, 6, 10, 17, 11, 2]
