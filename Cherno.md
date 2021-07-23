### 31.Arrays

**数组：基本上就是元素的集合，它是按照特殊顺序排列的一堆东西；在C++中，数组是连续存储大量数据，通常在同一时间在一行中；**

代码实例：

```c++
#include <iostream>

int main()
{
	int example[5];
	
	example[0] = 2;
	example[1] = 2;
	example[2] = 2;
	example[3] = 2;
	example[4] = 2;

	std::cout << example[0] << "  " << example << std::endl;

	std::cin.get();
}
```

**数组名实际上存储的是一个指针，数组通常需要用索引即`[]`中的数字来读取或者写入数据，索引从0开始；**由于数组中索引的原因，常常使用`for`循环来把数据写入数组中；

代码示例：

```c++
	int example[5];
	
	for (int i = 0; i < 5; i++)
	{
		example[i] = 2;
	}
```

由于数组名是一个指针，所以我们也可以用其他方式来读取和写入数组元素；

代码示例：

```c++
	int example[5];
	int* ptr = example;
	int* p = example;
	for (int i = 0; i < 5; i++)
	{
		example[i] = 2;
	}

	example[2] = 5;
	std::cout << example[2] << std::endl;

	*(ptr + 2) = 6;
	std::cout << example[2] << std::endl;

	*(int*)((char*)p + 8) = 7;
	std::cout << example[2] << std::endl;
```

**这里写入的位置为同一个，都是数组中的索引为2的元素，也就是数组中的第三个元素；这里指针所加的值实际为偏移量，偏移量为该指针类型的值所占的字节数乘以这个加的数；**

我们也可以在heap上用`new`关键字创建数组

代码示例：

```c++
	int example[5];
	for (int i = 0; i < 5; i++)
	{
		example[i] = 2;
	}

	int* another = new int[5];
	for (int i = 0; i < 5; i++)
	{
		another[i] = 2;
	}

	delete[] another;
```

**这里创建的数组example和another基本是一样的，除了存在的时间，数组example在数组所在域结束就不存在了，而数组another会一直存在，需要用关键字`delete`进行删除；**

*C++库中有一种内置数据结构叫做标准数组，它具有边界检查，跟踪数组大小等优势所在；使用这个标准数组需要包含头文件`#include <array>`；*

代码示例：

```c++
#include <iostream>
#include <array>

int main()
{
	std::array<int, 5> example;
	for (int i = 0; i < example.size(); i++)
	{
		example[i] = 2;
	}
	
	std::cin.get();
}
```

### 32.Strings

**字符串实际上是一组字符，字符是字母、数字、符号之类的；字符在C++中为char类型，而字符串在C++中基本上就是一个字符数组；**

代码示例：

```c++
#include <iostream>

int main()
{
	const char* name = "Cherno";
	std::cout << name << std::endl;

	std::cin.get();
}
```

这里的字符串在存储在内存中实际上会在最后一位字符的后面再加上一个空字符`'\0'`，这样可以使得在输出整个字符串时知道字符串的结尾在哪；

代码示例：

```c++
	const char name[10] = { 'C','h','e','r','n','o','\0','a','b','n' };
	std::cout << name << std::endl;
```

这里的输出结果实际上为`Cherno`；

**在C++标准库中有叫`string`的类，内包含一个标准字符串；**

```c++
#include <iostream>
#include <string>

int main()
{
	std::string name = std::string("Cherno") + " hello";
	std::cout << name << std::endl;

	std::cin.get();
}
```

可以使用以上的类似代码使用标准字符串；

### 33.String Literals（字符串字面量）

字符串字面量基本就是在双引号中的字符，例如`"hello"`，它默认为`const char*`类型，总是存储在只可读的内存片段，不可以去更改其中的字符，末尾有一个空字符`\0`来表示字符串何时结束；

```c++
	const char* name = "Cherno";
	name[2] = 'a';
	char name2[] = "Cherno";
	name2[2] = 'a';
```

第二行的代码是不会报错的，因为是一个`const char*`类型，但是第四行的不会报错，因为这里是复制一个`"Cherno"`的副本到数组中，所以可以对其中的字符进行更改；

C++中还有其他的字符串类型；

```c++
	const char* name = u8"Cherno";
	const wchar_t* name2 = L"Cherno";

	const char16_t* name3 = u"Cherno";
	const char32_t* name4 = U"Cherno";
```

默认`char`类型的前缀可以省略，但是其他字符串类型的前缀不可省略，因为在计算机中字符串字面量默认为8位的字符，而`char16_t`类型是字符占16位的字符串，`char32_t`类型是字符占32位的字符串，`wchar_t`类型的字符大小由编译器来决定；

也可以使用前缀R来让字符串字面量占多行；

```c++
	const char* example = R"(hello
world
tomorrow
will
better)";
```

### 34.`Const`关键字

可以声明整型为`const`，然后就是一个常量，此时不可更改这个整型的值

```c++
#include <iostream>
#include <string>

int main()
{
	const int a = 5;

	std::cin.get();
}
```

**`const`与指针一起用，有两种不同的用法，这两种用法可以结合起来使用**

```c++
	const int a = 5;
	const int* b = new int;
	b = &a;
//	*b = 7;
```

*此时不可以通过解引用指针来改变变量 `a`的数值，即第四行的代码会报错；*

```c++
	const int a = 5;
	int* const b = new int;
	*b = 7;
//	b = (int*)&a;
```

*此时不可以改变指针 `b`存储的地址变量，即第四行出错；*

```c++
	const int a = 5;
	const int* const b = new int;
//	*b = 7;
//	b = (int*)&a;
```

*此时既不可以更改指针 `b`中保存的地址，也不可以通过解引用指针来改变变量 `a`的数值，即三四行都会报错；*

`const`与引用

```c++
	int a = 8;
	const int& b = a;
//	b = 7;
```

*不可以通过该 `const`形容的应用改变变量`a`的数值；*

**`const`关键字与`class`类和`method`方法**

```c++
class Entity
{
public:
	int m_X, m_Y;
public:
	int GetX() const
	{
//		m_X = 2;
		return m_X;
	}
	int SetX(int x)
	{
		m_X = x;
	}
};
```

*注释掉的行中的代码不能使用，因为这个方法使用了 `const`形容，所以不可以改变类中的变量；*

### 35.`mutable`关键字

`mutable`实际上有两种截然不同的用途；

在类、方法中和`const`搭配使用

```c++
#include <iostream>
#include <string>

class Entity
{
private:
	std::string m_Name;
	mutable int m_DebugCount = 0;
public:
	const std::string& GetName() const
	{
		m_DebugCount++;
		return m_Name;
	}
};
int main()
{
	const Entity e;
	e.GetName();
	std::cin.get();
}
```

*这里的 `mutable`使得变量 `m_DebugCount`可以在这个方法 `GetName()`中改变；*

在lambda中搭配使用

```c++
	int x = 8;
	auto f = [=]() mutable
	{
        x++;
		std::cout << x << std::endl;
	};
```

这里使得传递到lambda中的变量可以改变；

### 36.Constructive Member Initializer Lists（构造成员初始化列表）

在构造函数中初始化我们的类成员函数，**强烈推荐使用这种方法来初始化成员；**

```c++
class Entity
{
private:
    int m_Score
	std::string m_Name;
public:
	Entity()
		: m_Score(10),m_Name("Unknown")
	{
	}
	Entity(const std::string& name)
		: m_Name(name)
	{
	}
	const std::string& GetName() const
	{
		return m_Name;
	}
};
```

*如果在类中有多个成员，那么需要按顺序来初始化成员；*

### 37.Ternary Operators（三元运算符）

三元运算符实际上就是一种选择语句的语法糖，实际用法如下

```c++
#include <iostream>
#include <string>

static int s_Level = 1;
static int s_Speed = 1;
int main()
{
	s_Speed = s_Level > 5 ? 10 : 5;
    
	std::cin.get();
}
```

等价于

```c++
	if (s_Level > 5)
		s_Speed = 10;
	else
		s_Speed = 5;
```

三元运算符可以和条件选择语句一样嵌套使用，但是最好不要去嵌套使用，会导致语句复杂；

### 38.实例化我们的类

通常有两种选择去实例化类

一、在stack（栈）中实例

```c++
#include <iostream>
#include <string>

class Entity
{
private:
	std::string m_Name;
public:
	Entity() :m_Name("Unknown") {}
	Entity(const std::string& name) :m_Name(name) {}

	const std::string& GetName() const { return m_Name; }

};
int main()
{
	Entity entity("Cherno");
	std::cout << entity.GetName() << std::endl;

	std::cin.get();
}
```

二、在heap（堆）中实例

```c++
	Entity* entity = new Entity("Cherno");
	std::cout << entity->GetName() << std::endl;

	delete entity;
```

通常在stack中创建对象比在heap中创建会快得多；

怎么选择用哪种方法来实例化类？

​	1.在类中的变量较多，占据的内存过大时在heap中实例化类，因为分配给stack的内存较小；

​	2.在需要对象存在的作用域之外使用对象时在heap中实例化类；

### 39.`new`关键字的语法

`new`关键词使用时一定要搭配着`delete`使用；

```c++
	int* b = new int[10];
	delete[] b;

	Entity* entity = new Entity();
	delete entity;
```

### 40.implicit conversion and the explicit keyword（隐式转换和显示关键字）

在C++中允许编译器对代码执行一次隐式转换

```c++
#include <iostream>
#include <string>

class Entity
{
private:
	std::string m_Name;
	int m_Age;
public:
	Entity(int age)
		:m_Name("Unknown"),m_Age(age) {}

	Entity(const std::string& name)
		:m_Name(name),m_Age(-1) {}
};
int main()
{
    Entity b(22);
	Entity a("Cherno");

	std::cin.get();
}
```

上面中实例化对象是常用的，实际上这里就有一次隐式类型转换，这里`"Cherno"`是字面量，为字符串常量类型，不是`string`类型，这里隐式转换为了`string`类型；

但是我们也可以通过明显的另一种方法去实例化对象

```c++
	Entity b = 22;
	Entity a = "Cherno";
```

第一行代码中，整型隐式转换为了`Entity`类型；但是第二行代码中由于`"Cherno"`为字面量，需要通过先转换为`string`类型，才能继续转换为`Entity`类型，所以会出错，因为隐式转换超过了一次，需要把代码改成如下才成成功；

```c++
	Entity a = std:string("Cherno");
```

可以通过在类前面增加显示关键字`explicit`使得不能通过隐式转换实例化对象；

```c++
	explicit Entity(int age)
		:m_Name("Unknown"),m_Age(age) {}
```

### 41.operators and operator overloading（运算符和运算符重载）

运算符重载定义或更改运算符的操作，看一下实际操作；

```c++
#include <iostream>
#include <string>

struct Vector2
{
	float X, Y;
	Vector2()
		:X(0), Y(0) {}
	Vector2(float x, float y)
		:X(x), Y(y) {}
	Vector2 Add(const Vector2& other) const 
	{
		return Vector2(X + other.X, Y + other.Y);
	}
	Vector2 operator+(const Vector2& other) const
	{
		return Add(other);
	}
	Vector2 Multiply(const Vector2& other) const
	{
		return Vector2(X * other.X, Y * other.Y);
	}
	Vector2 operator*(const Vector2& other) const
	{
		return Multiply(other);
	}
	bool operator==(const Vector2& other) const
	{
		return X == other.X && Y == other.Y;
	}

};
std::ostream& operator<<(std::ostream& stream, const Vector2& other)
{
	stream << other.X << ", " << other.Y;
	return stream;
}

int main()
{
	const Vector2 position(4.0f, 4.0f);
	const Vector2 speed(0.5f, 1.5f);
	const Vector2 powerup(1.1f, 1.1f);

	Vector2 result1 = position.Add(speed.Multiply(powerup));
	Vector2 result2 = position + speed * powerup;

	std::cout << "result1: " << result1 << std::endl;
	std::cout << "result2: " << result2 << std::endl;
	std::cout << (result2 == result1) << std::endl;


	std::cin.get();
}
```

通过运算符重载，这里我们可以对我们创建的对象使用符号进行操作；

### 42.`this`关键字

`this`关键字是所在方法所属的当前实例对象的指针，只可以在方法中被引用；

```c++
#include <iostream>
#include <string>

class Entity
{
public:
	int x, y;

	Entity(int x, int y)
	{
		this->x = x;
		this->y = y;
	}
	int GetX() const
	{
		return this->x;
	}
};

int main()
{
	Entity entity(5, 5);
	std::cout << entity.GetX() << std::endl;

	std::cin.get();
}
```

### 43.object lifetime （对象生命周期）

基于堆栈的变量和基于堆的变量的对象生命周期是不一样的，一旦超过变量所在的的作用域基于堆栈的变量就被释放；

```C++
#include <iostream>
#include <string>

class Entity
{
public:
	Entity()
	{
		std::cout << "Created Entity!" << std::endl;
	}
	~Entity()
	{
		std::cout << "Destroyed Entity!" << std::endl;
	}
};

int main()
{
	{
		Entity e;
	}
	std::cin.get();
}
```

如上面的代码中，会在创建对象的时候使用构造函数，会在出了作用域的时候自动使用删除函数；因此不要在函数中创建一个基于堆栈的变量，然后返回它的指针，这样很明显是错误的；

作用域指针（智能指针）代码示例：

```c++
#include <iostream>
#include <string>

class Entity
{
public:
	Entity()
	{
		std::cout << "Created Entity!" << std::endl;
	}
	~Entity()
	{
		std::cout << "Destroyed Entity!" << std::endl;
	}
};

class ScopedPtr
{
private:
	Entity* m_Ptr;
public:
	ScopedPtr(Entity* ptr)
		:m_Ptr(ptr)
	{
		
	}
	~ScopedPtr()
	{
		delete m_Ptr;
	}
};
int main()
{
	{
		ScopedPtr e(new Entity());
	}

	std::cin.get();
}
```

这里的类`ScopedPtr`对象是基于堆栈创建的，会在出了作用域的时候自动销毁，而这也导致自动使用了销毁函数中的`delete m_Ptr`语句来删除创建在堆上的`Entity`对象；

### 44.smart pointers（智能指针）

**智能指针意味着当您调用`new`关键字时，不用调用`delete`关键字；甚至不用调用`new`关键字；**

**unique pointer（唯一指针）：是一个作用域指针，意味着当该指针超出它所在的作用域的时候它将被销毁；且不能复制到另一个指针中去；**

```c++
#include <iostream>
#include <string>
#include <memory>

class Entity
{
public:
	Entity()
	{
		std::cout << "Created Entity!" << std::endl;
	}
	~Entity()
	{
		std::cout << "Destroyed Entity!" << std::endl;
	}
	void Print() {}
};

int main()
{
	{
		std::unique_ptr<Entity> entity(new Entity());
		std::unique_ptr<Entity> e = std::make_unique<Entity>();

		entity->Print();
		e->Print();
	}

	std::cin.get();
}
```

如上述代码，一般有两种方法创建唯一指针，通常使用这里面的第二种；

**shared pointer（共享指针）：通过引用计数跟踪您的指针有多少引用，当引用计数到零时，该指针被销毁；**

```c++
#include <iostream>
#include <string>
#include <memory>

class Entity
{
public:
	Entity()
	{
		std::cout << "Created Entity!" << std::endl;
	}
	~Entity()
	{
		std::cout << "Destroyed Entity!" << std::endl;
	}
	void Print() {}
};

int main()
{
	{
		std::shared_ptr<Entity> e0;
		{
			std::shared_ptr<Entity> shareEntity = std::make_shared<Entity>();
			e0 = shareEntity;
		}
	}


	std::cin.get();
}
```

可以通过在编译器中通过设置断点来查看具体运行情况；

**weak pointer （弱指针）：把一个共享指针分配给共享指针时，引用计数会增加，但是把一个共享指针分配给弱指针时，引用计数不会增加；弱指针仅仅只记录该对象的地址；**

```c++
	{
		std::weak_ptr<Entity> e0;
		{
			std::shared_ptr<Entity> shareEntity = std::make_shared<Entity>();
			e0 = shareEntity;
		}
	}
```

当弱指针引用的原指针被销毁的时候，弱指针指向一个空的指针，无实际意义；

### 45.coping and copy constructor（复制和复制构造函数）

在C++中复制通常是将一块内存中保存的二进制段直接复制到另一块内存中；

```c++
int i = 9;
int j = i;
j = 10;
std::cout << i << ", " << j << std::endl;
```

这里通过复制一块内存到另一块内存中把9赋值给`j`，改变`j`的值并不会改变`i`的值；

```c++
int* i = new int;
i = 9;
int* j = i;
j = 10;
std::cout << *i << ", " << *j << std::endl;
```

这里虽然同样也是把一款内存中的二进制段复制到另一块内存中，即复制指针到`j`中，但是因为`i,j`中保存的指针为同一个，所以输出会出现一样的值；

**复制构造函数：是复制自制类的一种好方法，因为类中通常会有指针，而直接复制一个类到另一个类中，在销毁其中一个类的时候会把之前分配给指针的内存也一起释放，这时另一个类就不能使用指针，因为已经在之前被释放掉了；**

```c++
#include <iostream>
#include <string>

class String
{
private:
	char* m_Buffer;
	unsigned int m_Size;
public:
	String(const char* srcString)
	{
		m_Size = strlen(srcString);
		m_Buffer = new char[m_Size + 1];
		memcpy(m_Buffer, srcString, m_Size + 1);
	}
	String(const String& other)
		:m_Size(other.m_Size)
	{
		m_Buffer = new char[m_Size];
		memcpy(m_Buffer, other.m_Buffer, other.m_Size + 1);
	}

	~String()
	{
		delete[] m_Buffer;
	}
	const char* GetString() const
	{
		return m_Buffer;
	}
	void AddEqual(const char* srcString)
	{
		char* tmp;

		m_Size += strlen(srcString);
		tmp = new char[m_Size];
		memcpy(tmp, m_Buffer, strlen(m_Buffer));
		memcpy(tmp + strlen(m_Buffer), srcString, strlen(srcString) + 1);
		delete[] m_Buffer;
		m_Buffer = tmp;
	}
	void operator+=(const char* srcString)
	{
		AddEqual(srcString);
	}
};
std::ostream& operator<<(std::ostream& stream, const String& string)
{
	stream << string.GetString();
	return stream;
}

int main()
{
	String name("gongzhihuang");
	String second = name;

	std::cout << second << std::endl;
	std::cout << name << std::endl;

	std::cin.get();
}
```

