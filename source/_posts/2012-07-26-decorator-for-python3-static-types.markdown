---
layout: post
title: decorator for python3 static types
date: 2012-07-26
comments: true
---

{% codeblock Here's an example .rvmrc file. lang:python %}
\
\#!/usr/bin/env python\
\#-\*- coding:utf-8 -\*-\

\

\

\
def accepts(\*types):\
    def check\_accepts(f):\
        print("len(types) = ", len(types))\
        print("f.func\_code.co\_argcount = ",
f.\_\_code\_\_.co\_argcount)\
        \# assert len(types) == f.func\_code.co\_argcount\
        def new\_f(\*args, \*\*kwds):\
            for (a, t) in zip(args, types):\
                assert isinstance(a, t), \\\
                       "arg %r does not match %s" % (a,t)\
            return f(\*args, \*\*kwds)\
        \# new\_f.func\_name = f.func\_name\
        new\_f.\_\_name\_\_ = f.\_\_name\_\_\
        return new\_f\
    return check\_accepts\
\
def returns(rtype):\
    def check\_returns(f):\
        def new\_f(\*args, \*\*kwds):\
            result = f(\*args, \*\*kwds)\
            assert isinstance(result, rtype), \\\
                   "return value %r does not match %s" % (result,rtype)\
            return result\
        new\_f.\_\_name\_\_ = f.\_\_name\_\_\
        return new\_f\
    return check\_returns\
\
@accepts(int, (int,float))\
@returns((int,float))\
def func(arg1, arg2):\
    return arg1 \* arg2\

\

{% endcodeblock %}

