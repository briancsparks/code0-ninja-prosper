---
title: "C++ Header Files"
date: 2020-09-06T17:20:48-07:00
draft: true
---

Assuming:

* foo: Class name
* bar: Library name
* baz: Owner or company name

### bar/foo.hpp

```h
#ifndef BAZ_BAR_FOO_H
#define BAZ_BAR_FOO_H

namespace baz {
  namespace bar {

    class Foo {

      public:
        int x,y;

        // Default c-tor
        Foo();

        // Copy c-tor
        Foo(Foo const & that);

        // Data c-tor
        Foo(int x, int y);

      protected:
        // Blah

      private:
        // Blah
    };

  };
};


#endif // BAZ_BAR_FOO_H
```
