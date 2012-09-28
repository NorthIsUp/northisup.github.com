---
layout: post
title: "The ternary operator in Python"
published: true
meta:
  aktt_notify_twitter: "yes"
  _edit_last: "2"
  aktt_tweeted: "1"
  btc_comment_counts: a:0:{}
tags:
- Code
- python
- Technology
- ternary
type: post
status: publish
---

{% highlight python %}
    # tl;dr for python >= 2.5
    b if a else c

    # tl;dr for python < 2.5
    (b,c)[not a]
{% endhighlight %}

What's a ternary operator? [Wikipedia can teach you!](http://en.wikipedia.org/wiki/Ternary_operation)

The ternary operator of C is one of my favorite operators, it may be hard to read at times, but oh so useful. The example reads "If a is true, then return b, else return c." The other examples will continue the use of `a` as the condition, `b` as the positive response and `c` as the negative response.

{% highlight c %}
    (a ? b : c)
{% endhighlight %}

#### for before python 2.5

In python you can do this in three ways, the third way is only available in python 2.5 and up. It is essentially a ternary operator and doesn’t require any complicated hacks. In these lambda function examples I am using a as the conditional, b as the true option and c as the false option:


{% highlight python %}
    (a and [b] or [c])[0]
{% endhighlight %}

This works due to the particular nature of and and or. The article is very good and goes in depth into the nature of and and or, specifically as to why this works. The reason that b and c are in brackets is because in some cases the b value can return False, but a list will always return True. Since we are returning a list we must reference the first element.

{% highlight python %}
    (b,c)[not a]
{% endhighlight %}

In this instance we rely on the fact that True == 1 and False == 0. This is important because we are using a conditional to access an element of the tuple. If a is True then not a will be false, or 0, thus accessing the first element. Similarly if a is False then not a will be True, or 1, and this will access the second element.

#### for python 2.5 and up

{% highlight python %}
    b if a else c
{% endhighlight %}

First a is evaluated, then either b or c is returned based on the truth value of a; if a evaluates to true b is returned, else c is returned.


#### examples

Here is an example of each form in action:

{% highlight python %}
    twoleg = ["human", "kangaroo"]
    fourleg = ["dog", "elephant"]
    animals = ["human", "kangaroo", "dog", "elephant"]

    print "Method one:"
    for c in animals:
        print "%s has %s legs"%(c, (c in twoleg and ["two"] or ["four"])[0])

    print "Method two:"
    for c in animals:
        print "%s has %s legs"%(c, ("two", "four")[c not in twoleg])

    print "Python 2.5+ only:"
    for c in animals:
        print "%s has %s legs"%(c, "two" if c in twoleg else "four")
{% endhighlight %}

