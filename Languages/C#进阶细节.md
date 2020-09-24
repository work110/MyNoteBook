# C#编码细节

# 容器类

## 数组【】

数组声明的时候就要指定长度，不能动态增加删减

### 声明

```c#
int[] data = new int[5];
int[] data = {1,1,1};
```



unity中,添加public修饰符之后，可以进行相关的编辑

```c#
public int[] _Array；
foreach(var i in _Array){ debug.log(i);}
```



### 类-数组的序列化

```c#
Book[] _books = new Book[5];

[System.Serializable]
public class Book{
	float _price;
	string _name;
    
    Book(float price,string name){
        _price = price;
        _name = name;
    }
}
```





## 列表List< >

列表可以动态添加删除元素

### 声明

```c#
public List<int> _list = new List<int>();

//添加元素
_list.Add(1);

//删除元素
_list.Remove(1);

```



### 类-列表的序列化

```c#
public List<Book> _list = New List<Book>();

_list.Add(book);
_list.RemoveAt(0);
```



## 字典

无重复值

### 声明

```c#
public Dictionary<int, Book> _dict = new Dictionary<int,Book>(); 

Book book1 = new book1(12f,"unity");

//添加元素
_dict.Add(0,Book1);

//遍历
foreach(var it in _dict){
    Debug.log(it.key);
    Debug.log(it.value._name);
}

//全部删除
_dict.Clear();

//按照key值删除
_dict.Remove(1);

//查找是否有某个值
_dict.ContainsKey(1);
_dict.ContainsValue(book1);
```



字典-类的序列化

在unity中不能序列化



## HashTable

哈希表继承自diction



## Stack栈

```c#
//建立栈
Stack stack = new Stack();

//入栈
stack.Push(1);
stack.Push("123");

//出栈
stack.Pop();

//先出123
```



# Nullable

可空类型的声明，可以为一个值指定为null值

```c#
bool? boolval = null;// 默认值为null
```



## 单问号？

对于int ，double，bool等无法直接赋值为null的数据类型进行null赋值，意为可空类型**Nullable**

```c#
int i ；		//默认值为0
int？ ii；	//默认值为null
```

定义一个可空类型的值

```c#
public enum State{
	None,idle,Run
}


public State? hlili'zi'aForceState{
	get;
	set;
}
```



## 双问号？？

判断变量为Null时返回一个指定的值

意为合并运算符，可以用于定义可空类型和引用类型的默认值

> a = b？？c    当b为空，等同于a =c

```c#
int? num1 = null;
int? num2 = 888;
int num3 = num1 ?? num2; //如果num1为空值则返回num2
```



# 类的修饰符



## public	公开的

类可以在任何地方访问



## private  私有的

只能由本类中的代码访问



## *internal  

只能由定义它的代码访问

类只能在当前工程中访问

> class A{} 即相当于 internal class A{}
>
> 通常省略



## protected	受保护的

只能由本类，或者派生类中的代码访问



## abstract	抽象的

不能实例化，只能继承



## sealed 	只能实例化的

不能被继承，只能实例化



# 方法的修饰符

## virtual 虚方法

可以在子类中被重写的方法



## abstract 必须在子类中被重写

如果一个类方法中有此修饰符，则class名前也必须添加abstract



## override 重载

子类的方法被重写，覆盖了一个父类的方法



## *extern 方法定义在其他地方



# new，this与base

子类的类方法

还可以使用new来隐藏基类的方法

通过this指向当前类实例引用

通过base关键字指向基类实例引用

# interface 接口

> abstract 与 sealed 不能在接口中使用，对接口毫无意义

> 当定义派生类时，如果有父类和接口，那么先写父类，然后再写接口，之前用逗号隔开

> 一个类只能有一个父类但是可以有多个接口
>
> 如：class Son：Father，IName，IFamily

## 定义

```c#
interface IMyInterface{

	void MethodToImplement()；

}
```



类的继承，直接继承重写接口方法即可



## 接口继承接口

如果一个接口继承了其他接口，那么继承了这个接口的类，需要实现所有的接口方法

```c#
interface IA{

	void MethodA();

}

interface IB{

	void MethodB();

}

class C:IA,IB{

	static void Main(){
	
	}
	
	public void MethodA(){
	
	}
	
	public void MethodB(){
	
	}

}
```















































