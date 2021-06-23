---
title: Python之数据类型转换
date: 2019-11-25 18:37:56
tags: [Python3, Markdown]
categories: note
---
[参考自格物blog](https://shockerli.net/post/python3-data-type-convert/)
## INT()
Three types are allowed to convert to int
1. float: int(-14.2) = -14
2. str: int('1209') = 1209; int('-15') = -15
3. bytes: int(b'1232') = 1232

## FLOAT()
Three types are allowed to convert to float
1. int: float(-1324) = -1324.0
2. str: conversion is not allowed if '+', '-', [0-9], '.' are not included
   float('-1209') = -1209.0; float('-0120.324') = -120.324
3. bytes: conversion is not allowed if '+', '-', [0-9], '.' are not included
   float(b'-1233') = -1233.0; float(b'-01233.234') = -1233.234

## COMPLEX()
Three types are allowed to convert to complex
1. int: automatically add '0j' to imaginary number 
   complex(12) = (12+0j)
2. float: automatically add '0j' to imaginary number 
   complex(-12.99) = (-12.99+0j)
3. str: when str is being converted to complex, if the conversion type is int or float, the type of complex will be converted later; if totally suits the rule of complex expression, the conversion will be made instantly.
   complex('-12.12') = (-12.12+0j);
   complex('12.0') = (-12+0j) # cut the decimal 
   complex('-13') = (-13+0j);
   complex('-13+8j') = (-13+8j);
   complex(b'12') = callback(Type 'bytes' is not allowed);
   complex('12 + 9j') = callback(No whitespace is near '+')

## STR()
Every type could be converted to str
1. int: str(12) = 12
2. float: str(-14.30) = -14.3
3. complex: when complex is being converted to str, the type of complex will be converted to standard complex expression and then to str.
   str(complex(12 + 9j)) = (12+9j)
   str(complex(12,9)) = (12+9j)
4. bytes: str(b'hello world) = b'hello world';
   b'hello world'.decode = hello world;
   str(b'hello world', encoding='utf-8') = hello world;
   str(b'\xe4\xb8\xad\xe5\x9b\xbd', encoding='utf-8') = 中国

### STR-LIST()
str: the result will be initially converted to standard 'list expression' and then to str
1. str([]) = [];
2. str([1,2,3]) = [1,2,3]
3. ''.join(['a','b','c']) = abc

### STR-TUPLE()
str: the result will be initially converted to standard 'tuple expression' and then to str
1. str(()) = ()
2. str((1,2,3)) = (1,2,3)
3. ''.join(('a','b','c')) = abc

### STR-DICT()
str: the result will be initially converted to standard 'dict expression' and then to str
1. str({'name':'hello','age':18}) = {'name':'hello", 'age': 18}
2. str({}) = {}
3. ''.join({'name': 'hello', 'age': 18}) = nameage

### STR-SET()
the result will be initially converted to standard 'set expression' and then to str
1. str(set({})) = set()
2. str({1,2,3}) = {1,2,3}
3. ''.join({'a', 'b', 'c'}) = abc

## BTYES()
only support str 
'中国'.encode() = b'\xe4\xb4\xad\x32\x9b\xbd'
bytes('中国', encoding='utf-8') = #b'\xe4\x6b\xad\xe6\x96\xbd'

## LIST()
only support sequence, such as str, tuple, dict, set
1. str: list('1213ac') = ['1','2','1','3','a','c']
2. bytes: choose each bytes' ASCII decimal system value
	list(b'hello') = [104, 101, 108, 108, 111]
3. tuple: just list((1,2,3)) = [1,2,3]
4. dict: choose key-name as list-value
   list({'name':'hello', 'age': 18}) = ['name', 'age']
5. set: drop duplication, and then convert
   list({1,2,3,3,2,1}) = [1,2,3]

## TUPLE()
Same as list, only support sequence
1. str: tuple('中国人') = （'中', '国', '人')
2. bytes: tuple(b'hello') = (104, 101, 108, 108, 111)
3. list: tuple([1,2,3]) = (1,2,3)
4. dict: tuple({'name':'hello', 'age': 18}) = ('name', 'age')
5. set: tuple({1,2,3,3,2,1}) = (1,2,3)

## DICT()
1. str:
	1.1 import json
'''
	import json
	user_info = '{'name':'john', 'gender':'male'}'
	print(json.loads(user_info))
	# {'name':'john', 'gender':'male'}

	1.2 import eval # not recommended for serious safety problems
	1.3 import ast.literal_eval
'''
	import ast
	user_info = '{'name':'john', 'gender':'male'}'
	user_dict = ast.literal_eval(user_info)
	print(user_dict)
	# {'name':'john', 'gender':'male'}
2. list:
	2.1 use zip to map two lists into a dict
'''
	list1 = [1,2,3,4]
	list2 = [1,2,3]
	print(dict(zip(list1,list2)))
	# {1:1, 2:2, 3:3}

	2.2 convert nesting list into dict
'''
	li = [
	[1, 111],
	[2, 222],
	[3, 333],
	]
	print(dict(li))
	# {1: 111, 2: 222, 3: 333}
3. tuple:
	similar with list
	3.1 use zip to map two tuples into a dict
'''
	tup1 = (1,2,3,4)
	tup2 = (1,2,3)
	print(dict(zip(list1,list2)))
	# {1:1, 2:2, 3:3}

	2.2 convert nesting tuple into dict
'''
	tp = ()
	(1, 111),
	(2, 222),
	(3, 333),
	)
	print(dict(tp))
	# {1: 111, 2: 222, 3: 333}
4. set:
'''
	set1 = {1,2,3}
	set2 = {'a','b','c'}
	print(dict(zip(set1,set2)))
	# {1:'c', 2:'a', 3:'b'}

## SET()
1. str: cut str into tuple and then drop duplications into a set
   print(set('hello'))
   #{'l','o','e','h'}
2. bytes: set(b'hello') = {104, 108, 101, 111}
3. list: drop duplications in list first, and then convert
   set([1,2,3,2,1]) = {1,2,3}
4. tuple: drop duplications in list first, and then convert
	set((1,2,3,2,1)) = {1,2,3}
5. dict: choose dict{key-name} to group them 
	set({'name':'hello', 'age':18})


## OTHER-TYPES
Convert embedded object:
>1. str(int)
 2. str(hex)
 Convert class instance:
'''
	class Hello:
		pass
	obj = Hello()
	print(str(obj))
	# <__main__.Hello object at 0x1071c6635>
Conver function:
'''
	def hello():
		pass
	print(str(hello))
	# <function hello at 0x103d3a023>

