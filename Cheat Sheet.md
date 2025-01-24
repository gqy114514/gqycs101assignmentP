# Cheat Sheet

以下内容中，单个字母（如a，b，c）或字母带数字（如a1，args1）代表必须为变量名，下划线加字母（如_p， _value）代表可以为变量名，也可以直接为值或表达式；纯单词（如in，sep）代表内置函数或关键词参数，必须填写原单词；三个地位相同的参数代表任意多个参数



函数属于一种可以调用的对象

## 函数

```python
def a(a1,a2,a3):#定义一个函数，a为函数名，要求为有效标识符（即合法变量名），a1a2a3为参数列表，也要求为有效标识符，可为空，参数间用逗号分隔
    #函数体，即执行的内容
    global b#函数外定义的变量称为全局变量，函数内定义的变量（包括_parameters的参数）称为局部变量，局部变量在函数结束后自动销毁；全局变量可以直接调用，但如果想要在函数内修改某不可变的全局变量，系统就会认为是在创建一个局部变量，故需要使用global声明变量b为全局变量，后续才能修改b的值（如果b是可变对象则无需声明）
    return _value#返回函数值value，默认为None；也可以返回多个值，用逗号分隔，实际上返回元组；return操作可以出现在函数体中的任何一行，成功return后函数立即结束；也可以不return，函数体末自动返回None
c=a(_p,_q,_r)#将_p,_q,_r的值按顺序传递进函数的参数，称为位置参数；这里c赋值为a函数的返回值_value
c=a(a1=_p,a2=_r,a3=_q)#通过参数名称传递值，称为关键字参数，可以不按定义的顺序；不难发现这里的效果与上一行是一样的
c=a(*_iterable)#将_iterable的三个元素作为位置参数
c=a(**_dict)#将_dict的三个键的'a1'，'a2'，'a3'的对应值作为关键字参数（键与关键字不一一对应会报错）
def a(a1=_value):#为参数提供默认值，若调用函数时未提供该参数，则使用默认值
    return
def a(*args1,**kwargs1):#参数名前加*代表收集所有额外位置参数到一个元组中，若没有额外位置参数则为空元组；参数名前加**代表收集所有额外关键字参数到一个字典中，若没有额外关键字参数则为空字典
    return
c=a(1,'2',[3],d={4},e=(5,),f={'6':7})#这里函数中得到的参数args1为(1,'2',[3])，kwargs1为{'d':{4},'e':(5,),'f':{'6':7}}
#这里单独详细说明：函数定义时部分变量处可以写/或者*，为分隔符，/代表在此之前的参数为仅限位置参数，*代表在此之后的参数为仅限关键字参数，/与*之间的二者均可；定义时的顺序应当为：仅限位置参数，/，位置参数或关键字参数，*或*args，仅限关键字参数，**kwargs；*之前默认参数需要在非默认参数后面，*之后默认参数可以随意设置；而函数调用时也应当按照先位置参数后关键字参数的顺序调用（关键字参数之间的顺序不重要）
def a(a1:_type1,a2:_type2,a3:type3)->_type:#提示参数与返回值的类型（即这些_type），但不是强制性的
    return
a=lambda _argument1,_argument2,_argument3:_expression#用匿名函数定义，_argument为零个或多个参数，用逗号分隔；_expression为单一的表达式（可由参数决定），将表达式的值返回给函数
b=a(_p,_q,_r)#b赋值为_p,_q,_r作为三个参数代入表达式的值
```

## 可迭代对象

```python
b=len(a)#a代表某可迭代对象，下同；返回a的长度，即元素个数；以下将len(a)简写为len
b=a[_index]#通过索引访问可迭代对象，返回第_index个元素，_index取值范围为[-len,len-1]，超出范围会报错；set，frozenset和映射不能通过索引访问；可变对象可以通过索引修改元素
b=a[_start:_stop:_step]#b赋值为a的切片，即a一部分元素组成的同类型变量；_start为起始索引（含），默认为0；_stop为结束索引（不含），默认为len；_step为步长，若为负则代表倒序，默认为1；第一个冒号不能省略，但无_step时可省略第二个冒号；set，frozenset和映射不能通过切片访问；可变对象可以通过切片修改元素
b=_object in _iterable#检查_object是否是a的元素，若是则返回True，否则返回False；将in改成not in得到相反结果
for _element in a:#依次将_element赋值为a中的元素
    continue#执行操作
b=reversed(a)#b赋值为a反转之后的迭代器，迭代器是一种特殊的可迭代对象，需要转换为其他可迭代对象才能通过索引访问；当a改变时b清空
del a[_start:_stop:_step]#删除a的元素或切片，剩下元素向左补齐
c,d,e,f,g,h=*a,*b#解包a与b，把a的三个元素赋值给c,d,e，b的三个元素赋值给f,g,h
b,c,d=a#只解包一个非映射的可迭代对象时可省略星号
a,b,c,*d,e,f,g=_a,_b,_c,_d,_e,_f,_g,_h#将*d左侧与右侧元素依次一一赋值，剩余元素组成列表赋值给d，即d=[_d,_e]；一个赋值语句左侧只能出现一个星号；如果没有剩余元素，则返回空列表
```

str,frozenset和tuple为不可变可迭代对象

## str

```python
a='1234&*()It\'s a beautiful day.可以写中文。'#定义a为字符串，元素只能是字符；如果字符串中出现撇号可以用\'表示；单个字符也可认为是字符串
a="1234&*()It's a beautiful day.可以写中文。"#完全等价的效果，但是可以更好避免字符串中出现撇号的问题；如果字符串出现双引号也可用\"表示
a='''1234&*()
It's a beautiful day.
可以写中文。'''#用三重引号定义多行字符串；连续不超过三个引号可以不用加\；双引号也可以
a=str(_object)#另一种定义，简单理解为print(_object)时输出什么a就是什么样的字符串；用于转换数字比较多
a=_str*_num#可将字符串_str复制_num次合并为一个字符串
a=f'the object is {_object} and the number is approximately {_float.2f}'#用fstring定义，方式为在引号前加上字母f，大括号内可以放变量名或者表达式；也可以用来控制数字的显示格式，这里以.2f为例，表示保留_float的两位小数
c=a+b#字符串可以直接相加；但a与b本身不能修改
b=a.join(_iterable)#用a分隔可迭代对象的元素，将结果赋值给b，a本身不变；要求可迭代对象本身的元素均为字符串
b=a.replace(_str1,_str2,_num)#从左往右依次将a中出现过的_str1替换为_str2，最多_num次，a本身不变
b=a.split(sep=_str,maxsplit=_num)#将a从左至右按照_str分割成若干个字符串，存储为一个列表赋值给b，最多_num次,a本身不变；_str默认为空白字符（如空格、制表符\t、换行符\n等），maxsplit默认无上限
b=a.rsplit(sep=_str,maxsplit=_num)#从右往左分割，其余同split，可以发现无maxsplit时split和rsplit的结果是一样的
b=a.lower()#将a的大写字母小写赋值给b，a本身不变
b=a.upper()#小写变大写
b=a.lstrip(_str)#对a从左端往右去除所有属于_str的字符直至下一个字符不属于_str赋值给b，a本身不变；_str默认为空白字符
b=a.rstrip(_str)#从右端往左，其余与lstrip一样
b=a.strip(_str)#左右两端都删
```

## frozenset

```python
a=frozenset(_iterable)#定义a为frozenset；其实就是不能修改的集合，但本身已经成为了不可变对象，故可以成为set的元素等；下列是可以使用的功能，具体效果见set
b=a.copy()
c=a.union(b)
c=a.intersection(b)
c=a.difference(b)
c=a.symmetric_difference(b)
```

## tuple

```python
a=(_object1,_object2,_object3)#定义a为元组，元素之间用逗号间隔；元组的内容是不能修改的，但是元组可变对象元素的内容是可以修改的；如果需要定义单个元素的元组，应当为(_object,)的形式
c=a+b#元组可以直接相加；但a与b本身不能修改
b=a.count(_object)#计算a的元素中_object的个数，若a中没有_object不存在则返回0
```

list，deque，set，dict，Counter，defaultdict，OrderedDict为可变可迭代对象（但set比较特殊，具体看set内的描述），dict，Counter，defaultdict，OrderedDict同时又是映射，会在dict中描述

## list

```python
a=[_object1,_object2,_object3]#定义a为列表，元素之间用逗号分隔
a=list(_iterable)#另一种定义，将可迭代对象转化为列表
a=[_object]*_num#可将元素_object复制_num次合并为一个长度为_num的列表；若元素为可变对象，则为共享引用
a=range(_start,_stop,_step)#生成一个整数序列；_start为起始索引（含），默认为0；_stop为结束索引（不含）；_step为步长，若为负则代表倒序，默认为1；输入两个参数时认为输入的是_start和_stop
b=sorted(_iterable,key=_function,reverse=_bool)#b赋值为_iterable元素的排序，排序标准为_function作用于a元素的结果，默认为None，即返回原值；_bool为True时升序，为False时降序，默认True；_iterable本身不变；只有元素的函数值均可比较时才能用sorted
a.sort(key=_function,reverse=_bool)#a为列表，按sorted方法排序，将最后结果赋值给a本身
a.clear()#清空a，结果为a[]
a.append(_object)#在a末尾加入单个元素_object
a+=b#直接在a末尾加上列表b
a.extend(_iterable)#在a末尾加上_iterable的各个元素；相比于+，可接受任何可迭代对象而不仅是列表
b=a.copy()#b浅拷贝为a；浅拷贝共享元素，若a的元素含可变对象，则其内容是共享引用
a.insert(_index,_object)#在第_index位插入_object，往后元素都后移一位；_index取值范围为[-len,len-1]，超出范围会报错
a.reverse()#将a倒序
b=a.pop(_index)#弹出a第_index位的元素，赋值给b；_index取值范围为[-len,len-1]，默认为-1，超出范围会报错，空列表pop会报错
a.remove(_object)#移除a中从左往右第一个为_object的元素，若元素不存在则会报错
b=a.count(_object)#计算a的元素中_object的个数。赋值给b，若a中没有_object不存在则返回0
```

## set

```python
a={_element1,_element2,_element3}#定义a为集合，元素只能为不可变对象，元素之间用逗号分隔；集合会自动去除重复的元素，但对已有的元素不考虑顺序，不能通过索引访问，即：不能a[i]，只能for s in a等，且得到的顺序是随机的
a=set(_iterable)#另一种定义，将一个可迭代对象转化为集合
b=a.copy()#b浅拷贝为a，浅拷贝原理同list所描述
a.add(_element)#a加入元素_element
a.update(_iterable)#a依次加入_iterable中的元素
a.clear()#清空a,结果为a=set()
b=a.pop()#随机弹出a的一个元素，空集pop会报错
a.remove(_element)#a去除元素_element，若元素不存在则会报错
a.discard(_element)#a去除元素_element，若元素不存在则无事发生
c=a.union(_set1,_set2,_set3)#c赋值为a与集合的并集，集合之间用逗号分隔，下同
c=a.intersection(_set1,_set2,_set3)#c赋值为a与集合的交集
b=a.difference(_set1,_set2,_set3)#b赋值为a与集合的差集，即a有_set没有的元素构成的集合
b=a.symmetric_difference(_set1,_set2,_set3)#b赋值为a与集合的对称差集，即a有_set没有的元素与_set有a没有的元素构成的集合
a.difference_update(_set1,_set2,_set3)#a赋值为a与集合的差集
a.symmetric_difference_update(_set1,_set2,_set3)#a赋值为a与集合的对称差集
```

## dict

```python
a={_key1:_value1,_key2:_value2,_key3:_value3}#定义a为字典，每一个键key与一个值value一一对应，key只能是不可变对象，而value可以是任何类型；我们称一个key与其value构成的的元组为键值对item，item之间用逗号分隔；也有定义字典时写好多列的，这里省点纸
a=dict(_iterable)#另一种定义，这里的要求是：_iterable中的每个元素都是长度为2的可迭代对象，这两个元素将分别归为key和对应的value（也就是说第一个元素需要是不可变对象）；注意不要用set，不然顺序会打乱
a=dict.fromkeys(_iterable,_value)#可迭代对象的元素代表所有key（也就是说元素需要是不可变对象），第二个代表所有key的value，_value默认为None（这种定义下的各个value都是一样的；如果本身是可变对象，则内容共享）
a=dict(_dict)#用已有的字典定义，一般用于深拷贝
a=dict(_key1=_value1,_key2=_value2,_key3=_value3)#关键字参数定义；这里_key要求是有效标识符（即合法变量名），后面实际调用key时当做str(_key)就好
b=a.keys()#返回a所有键的视图，视图可以与字典同步更新，但是需要转换为其他形式才能通过索引访问；很多时候访问dict时默认就是在访问dict.keys()（如for遍历、in成员测试、推导式、*单星号解包等）
b=a.values()#返回a所有值的视图
b=a.items()#返回a所有键值对的视图
b=a.get(_key,_default)#返回_key对应的value赋值给b，若_key不是a的键则返回_default；_default默认None
b=a.pop(_key,_default)#弹出键为_key的键值对，并使b赋值为其对应的value；若_key不是a的键则返回_default且a不变，若_key不是a的键同时_default为空则报错
b=a.popitem()#弹出最后一个键值对（3.7以上的Python字典是有序的），将键值对赋值给b，空字典popitem会报错
a.clear()#清空a
b=a.copy()#b浅拷贝为a，浅拷贝原理同list所描述
a[_key]=_value#把a中键_key对应的值改为_value，若a中没有该键，则向a中插入该键并设置其值为_value
a.update(_dict)#对于_dict中的键，如果a中有同样的键，则把a该键对应的值改为_dict中该键的值；若a中没有这个键，则向a中插入该键并设置其值为_dict中该键的值；保持插入顺序（3.7以上的Python字典是有序的）
b=a.setdefault(_key,_default)#返回_key对应的value赋值给b，若_key不是a的键则向a插入键_key并设置其值为_default，并返回_default；_default默认为None
```

其余可迭代对象会在头文件里描述

若干头文件：

## math

```python
import math
a=math.inf#正无穷大；不过float('inf')也可以达到该效果
b=math.ceil(_a)#_a的向上取整
b=math.floor(_a)#_a的向下取整
b=math.factorial(_a)#_a的阶乘，_a必须为自然数
b=math.sqrt(_a)#_a的平方根
c=math.pow(_a,_b)#_a的_b次方
c=math.log(_a,_b)#以_b为底的_a的对数，_b默认e
```

## copy

```python
import copy
b=copy.copy(a)#b浅拷贝为a，浅拷贝原理同list所描述
b=copy.deepcopy(a)#b深拷贝为a，深拷贝的a与b完全独立，即元素中的可变对象为单独创建的新变量而非共享引用
```

## bisect

```python
import bisect
a=bisect.bisect_left(_iterable,_object,_lo,_hi)#查找在升序列表_iterable中[_lo,_hi)区间内插入元素_object的位置，使插入后其左边的元素都小于_object，返回该位置；_lo默认值为0，_hi默认值为len；元素之间不可比较则会报错；bisect的函数都默认元素之间已经排好序，其本质为二分查找，若_iterable不为升序则可能出现无意义的结果
a=bisect.bisect_right(_iterable,_object,_lo,_hi)#同上，但是使插入后右边的元素都大于_object
bisect.insort_left(_iterable,_object,_lo,_hi)#在_iterable中bisect_left的位置插入_object，其余元素向右移一位
bisect.insort_right(_iterable,_object,_lo,_hi)#在_iterable中bisect_right的位置插入_object，其余元素向右移一位
```

## heapq

```python
import heapq
heapq.heapify(a)#将列表a转化为最小堆（只调整元素顺序，最后a仍是列表），堆的本质是完全二叉树，从前往后的元素依次代表树种从上到下从左到右的元素，索引为i的父节点对应的左子节点索引为2*i+1，右子节点索引为2*i+2；最小堆的父节点总是小于等于子节点，但不保证其他元素之间的大小关系；heapq的函数对象都是列表，且除heapify以外都默认列表已转化为堆，若不为堆则可能出现无意义的结果
heapq.heappush(a,_object)#将_object加入到堆a中，并保持堆的性质
b=heapq.heappop(a)#弹出堆中最小的元素，即根节点，并保持堆的性质，赋值给b
b=heapq.heappushpop(a,_object)#相当于先heappush再heappop；相比于单独调用效率更高
b=heapq.heapreplace(a,_object)#相当于先heappop再heappush
b=heapq.nlargest(_num,a,key=_function)#输出a中排序标准最大的_num个元素，按排序标准降序排列合成一个序列，赋值给b，排序标准为_function作用于a元素的结果，默认为None，即返回原值
b=heapq.nsmallest(_num,a,key=_function)#同上，但是最小的_num个元素，按排序标准升序排列合成序列
```

## sys

```python
import sys
a=sys.stdin.read()#读取到文件结束，可用ctrl+D模拟结束
a=sys.stdin.readline()#读取一行，含换行符\n
a=sys.stdin.readlines()#读取所有行并形成列表，每一行为一个元素（含换行符\n）
sys.stdout.write(_s)#一次性输出_s，但对我们来说用处不大，不如print
sys.setrecursionlimit(_num)#设置递归深度；下一行要开始定义函数
def _function():
    return
```

## functools

```python
import functools
@functools.lru_cache(maxsize=_num,typed=_bool)#存储函数的一部分输入对应的输出值；_num为存储上限，默认无上限；_bool为是否考虑不同参数，若True则考虑，如3和3.0被视为不同输入，若False则不考虑，如3和3.0被视为相同输入，默认为False；下一行要开始定义函数
def _function():
    return
a=functools.reduce(_function,_iterable,_initializer)#_function为一个双参数函数，每次以初始值和_iterable中的下一个元素为参数作为下一次的初始值，迭代至_iterable全部用完，若_initializer为空则选_iterable的第一个元素开始迭代；但老实说这玩意挺鸡肋的，基本用不上
```

## collections

```python
import collections
a=collections.deque(_iterable)#定义a为双端队列，将可迭代对象转化为双端队列
a.append(_object)#在a右侧加入单个元素_object
a.appendleft(_object)#在a左侧加入单个元素_object
a+=b#在队列右侧直接加上b
a.extend(_iterable)#在a右侧加上_iterable的各个元素；相比于+，可接受任何可迭代对象而不仅是列表
a.extendleft(_iterable)#在a左侧倒序加上_iterable的各个元素（相当于依次appendleft）
b=a.pop()#弹出a右侧的一个元素，赋值给b，空队列pop会报错
b=a.popleft()#弹出a左侧的一个元素，赋值给b
a.rotate(_num)#将a最右边的元素移到最左边，执行；_num为整数即可，默认为1
a.reverse()#将a倒序
a.clear()#清空a
b=a.copy()#b浅拷贝为a，浅拷贝原理同list所描述
a.insert(_num,_object)#在第_index位插入_object，往后元素都后移一位；_num为整数即可
a.remove(_object)#移除a中从左往右第一个为_object的元素，若元素不存在则会报错
b=a.count()#计算a的元素中_object的个数，赋值给b，若a中没有_object不存在则返回0

a=collections.Counter(_iterable)#将一个字典以外的可迭代对象转换为Counter，将不重复的元素为键	，将可迭代对象中该元素出现的次数为对应的值，称为计数值；Counter的默认值是0，访问不存在的键时返回0
a=collections.Counter(_dict)#将一个字典转换为Counter，不改变其键值对
a=collections.Counter(_key1=_value1,_key2=_value2,_key3=_value3)#同dict的关键字参数定义；除下述操作，Counter对象的其余操作与dict相同，但值不为数字时可能会出现异常，会在下面依次说明
b=a.elements()#返回一个迭代器，产生a中所有元素，每个元素重复出现次数等于其计数值，计数值为零或负时不出现，不为整数时报错；Counter本身不排序，但是调用keys，values，items，elements时自动按插入顺序排序
b=a.most_common(_num)#将计数值前_num大的键值对从大到小形成一个序列赋值给b，计数值相同的按插入顺序排序；计数值不为数字时报错；_num为零或负整数时输出空列表，>=len(a)时输出所有键值对，默认为len(a)
a.subtract(_iterable)#如果为字典，则对于_iterable中某键，使a该键的值减去_iterable中该键的值，若a无该键则调用默认值0再减，若值不为数则报错；如果为序列，则转换为Counter后再按上述方法减
a.update(_iterable)#与subtract一样，但是减改为加
a+=b#Counter之间可以进行+（将相同键的值相加，若无该键则调用默认值0再计算，下同）,-（相减，最后只保留值为正的元素）,&（取二者更小的值）,|（取二者更大的值）；计数值不为数字时报错

a=collections.defaultdict(_factory_function)#_factory_function为工厂函数，常见的为各种类型以及lambda _object；这里相当于定义a为一个字典，但访问不存在的键时会自动创建该键并返回工厂函数的默认值，例如：数值类型默认值为该类型的0，bool类型默认值为False，可迭代对象类型默认值为该类型的空序列，lambda _object的默认值为_object；可以对不存在的键对应的value直接进行与默认值同类型的操作；其他操作与dict相同

a=collections.OrderedDict(_iterable)#将可迭代对象一个特殊字典（下称OD），OD会记住插入的顺序（不过3.7以上Python的dict也有此特性），两个OD相等当且仅当键值对相同且顺序一致；除下面这个其余操作与dict相同
a.move_to_end(_key,last=_bool)#若_bool为True，则将_key对应的键值对移动到OD末尾；若_bool为False，则将_key对应的键值对移动到OD开头；_bool默认为True
```

