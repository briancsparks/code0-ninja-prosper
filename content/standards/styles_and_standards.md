---
title: "Coding Styles and Standards"
date: 2020-09-06T20:06:31-07:00
weight: 10
---

The code presented here has to follow a coding style of one type or another, and there
are many to choose from. After looking into industry best practices and pros and cons
of various styles, I ended choosing 'none of the above.' This site is a place to get a
starting template for your code, so you should style it according to your own style
standards. Most modern coding editors and IDEs will automatically do this for you, anyway.

However, just for completeness sake, here is the style / standard that the code on this
site uses.

If your team doesn't have a codeing style guide, feel free to use this one. (The value to
the team of having a coding standard is that you can stop arguing about what your coding
standard should be, and just get back to work.)

### All Languages

1. Do what is right / best.
   * Sometimes, breaking the standard leads to much more understandable code. In those
     cases, just do what is right.
1. The code on this site is intended to be copy-pasted by the user, so try to write
   it in a way that modern editors can understand, so that the user is unburdened.
1. Use two space tabs; never use tab characters.
1. Do your best to match parentheses and all their ilk within every file.

### C and C++ Specific

1. Always initialize variables as they are being declared.
1. ALL_CAPS names are for pre-processor items.
1. Put `const` and `volatile` on the right side of the type. (`char const * sz`)

#### Notes - All Languages

1. Two space tabs.
   * Studies have shown that code is understood by the reader best if it is written with
   either 3, or 2, or 4 space tabs, in that order, meaning that 3 space tabs are understood
   best, followed by 2 and 4, and then all the others (which all fared quite badly.)  This all
   means that you really should one of these three indents, but it really doesn't matter
   which. On the other hand, 3 is just weird, and 4 can lead to lines ending at very high column
   numbers. So, this site uses 2.
1. Matching.
   * Many code editors may get confused otherwise. You would rather have your editor doing
     its job well than being gramatically correct in your comments.
   * This mostly means to watch how you use the speical matched-pair symbols inside strings
     and comments. Many times this leads to some weirdness for the reader.
   * Dont use apostrophes. The code editor might see it as the beginning of a string. This can
     lead to comments that seem _just wrong_, like the first sentence in this paragraph.
   * Sometimes, you have to add the matching item inside a comment.

#### Notes - C and C++

1. Initialize variables.
   * Do not let **uninitialized variable** bugs into your code. If you initialize all variables
     as they are declared, they cannot creep in.
   * C and C++ do not set new variables to zero, unlike all other languages. Most developers
     understand that variables must be set before they are read, but many times see the
     declaration of variables as _bookkeeping_, not as part of the correctness of the code,
     so a lot of code is written without initialization. When the code is initially written,
     the developer will have tested things, but after the original creation phase, code
     changes. This is when **uninitialized variable** bugs creep in.
   * Code on this site will usually initialize variables to zero, even if the first meaningful
     value is different. This just makes it clear that the variable is being initialized for
     initialization's sake.
   * The first time you don't waste two weeks tracking down an **uninitialized variable** bug,
     you will more than make up for any hastle this item presents.
   * Once you are a lead developer, any time you are put onto an existing project, institute
     this rule and force the team to spend a day instituting it. You will be a hero, as you
     will have just fixed all those nagging bugs in the bugbase that just say 'weird things
     happen when you do x,y.z'.
1. ALL_CAPS names are for pre-processor items and should not be used to communicate const-ness.
   * From day one, C has used ALL_CAPS for `#define` tokens, which are usually just constants,
     so developers got used to ALL_CAPS meaning const-ness. But this is not right. ALL_CAPS is
     a hint to the reader that the item behaves by a different set of rules than all the other
     code. The item will be expanded by a dumb text processor, which might wreak havoc on the
     syntax of the code it is expanded into.
1. Put cv-qualifiers after the type.
   * I.e. `char const * sz`
   * Makes it so that reading from right-to-left tells you what you have. So, `sz` is:
     * Pointing to a constant character (the `char` cannot change.)
   * As opposed to what you would think reading it naturally. `const char * sz` seems to mean:
     * A constant character-pointer. (A pointer that cannot change, which is wrong.)

