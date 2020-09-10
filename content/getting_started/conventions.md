---
title: "Conventions"
date: 2020-09-06T18:35:25-07:00
weight: 20
---

Our intention is to provide content that you can use as-is without forcing you to find the
missing parts of what you are looking for. We had to make a few decisions on what the
templates would look like, so here is what we chose, and why.

### Templating Engine

Rather, the lack thereof.

There are a bazillion templating engines we could have chosen from, but we decided not to
use any, but to instead to use 'meta words' like `foo`, `bar`, `baz`, with the hopes that you would
only have to do a simple text copy-and-paste for your needs. For example, a simple template
for a C++ header is shown below.

* Valid as-is.
* Easy to transform for your needs.
  * Replace 'Foo' with your class name, and 'FOO' with the UPPERCASE version of it.
  * Replace 'bar' with your namespace, and 'BAR' with the UPPERCASE version of it.

```cpp
#ifndef __BAR_FOO_HPP__
#define __BAR_FOO_HPP__

namespace bar {
  class Foo {
  public:

    // Default c-tor
    Foo();
    
    // Copy c-tor
    Foo(Foo const & that);
    
    // etc.
  };
};

#endif // __BAR_FOO_HPP__
```
