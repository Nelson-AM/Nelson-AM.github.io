---
layout: post
title: "Python's Import Intricacies"
date: 2019-06-04 12:00:00
categories: blog, programming
---

So far, most of my python projects have consisted of single files, only importing external packages. Now that I'm more focused on test-driven development and developing my skills in a more structured way, I find I'm splitting up my logic between multiple files. This requires relative imports within and between the packages and modules I write. Last week, I realised I didn't know how to properly, Pythonically, import stuff from another file.

<!-- more -->

Relative imports in Python weren't directly obvious to me and looking at the number of questions on StackExchange about this topic, I don't seem to be the only one. Most of these questions are rather old and the answers often involve changing sys.path, the PYTHONPATH, or using other seemingly clunky methods. I explored a number of different options that seemed to make sense to me as well as suggestions I found on StackExchange. In doing this, I ran into some import intricacies that I'd like to share.

Suppose, I have the following directory structure and want to test `source.py`'s `sample_function` in `testsource.py`.

```python
pythonpackage/
├── __init__.py
├── food.py
└── test_food.py
```

`food.py`:

```python
def spam_is_food():
    return 1
```

`test_food.py`:

```python
import unittest

class TestFood(unittest.TestCase):
    def test_if_spam_is_food(self):
        self.assertEqual(spam_is_food(), 1)
```

Even though both modules are in the same package, `sample_function` needs to be imported in order for it to be found by the test case. Below is a list of the suggestions from StackExchange and other things I tried, with my commentary on it.

* Using `import food` and calling `spam_is_food()` regularly does not work. This feels the most intuitive.
* Using `import food as f` and then calling `f.spam_is_food` works (test succeeds), but PyCharm complains that there's no module `food`. This feels a bit clunky, but it can prevent potential naming conflicts between packages.
* Using `from food import spam_is_food` works, but PyCharm complains about unresolved references for both `food` and `spam_is_food`. Python seems to recognise that the module is there, but I'm not sure why PyCharm is complaining about it. Since both files are in the same package, I would expect this to work like a charm.
* Using `from pythonpackage import food` and calling `spam_is_food` does not work, and that's a shame given that the above option does work.
* Using `from pythonpackage import food as f` and calling `f.spam_is_food` works without complaints from PyCharm. This is the most clunky of the five and doesn't make me happy.

Having tried all this, I decided to refine my search queries. Lo and behold, I finally found [pep-328](https://www.python.org/dev/peps/pep-0328/) which contains [Guido's Decision](https://www.python.org/dev/peps/pep-0328/#guido-s-decision) on relative imports, and I think it provides a good middle-ground solution. So, the correct way to import `spam_is_food` from `food.py` in this structure is to: `from .food import spam_is_food`.

## Further Reading

Here, I'm only scratching the surface of Python's import system. There's a lot to learn about modules, packages and namespaces, so I've included some further reading that I will explore:

* [The Import System (Python 3 Docs)](https://docs.python.org/3/reference/import.html)
* [Modules (Python 3 Docs)](https://docs.python.org/3/tutorial/modules.html)
* [Absolute vs. Relative Imports](https://realpython.com/absolute-vs-relative-python-imports/)
* [Python Modules - An Introduction](https://realpython.com/python-modules-packages/)
