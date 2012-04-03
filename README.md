## Rudimentary key-value coding (KVC) for Python 2.x

This does not do everything that Apple's KVC does but it
may however be useful to somebody so here you go!

---

This module lets you set/get attribute values by walking
a "key path" from a root or start object.

A key path is a string with path part specs delimited by period '.'.
Multiple path part specs are concatenated together to form the
entire path spec.

Each path part spec takes one of two forms:

- identifier
- identifier[integer]

Walks proceed by evaluating each path part spec against the
current object, starting with the given object.

Path part specs work against objects, lists, tuples, and dicts.

Note that a KeyError or IndexError encountered while walking a
key path part spec is not caught. You have to know that the a
walk of the given key path on the given object will work.

An example walk:

    class A(object):
        def __init__(self):
            self.x = dict(y=['hello', 'world'])

    class B(object):
        def __init__(self):
            self.a = A()

    b = B()
    print value_for_keypath(b, 'a.x.y[1]')  # prints 'world'

    # part spec    context
    # ---------    -------
    # 'a'          b.a
    # 'x'          b.a.x
    # 'y[1]'       b.a.x.y[1]

