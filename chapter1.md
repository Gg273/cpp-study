#### 1.1 编写一个简单的程序

​	每个c++程序都包含一个或多个函数（function），其中一个必须命名为**main**，操作系统通过调用main函数来运行程序。一个函数的定义包好四部分：**返回类型**（return type）、**函数名**（function name）、**形参列表**（parameter list，允许为空）以及**函数体**（function body）。

例如：

```c++
int main()
{
    return 0;
}
```

​	这里的main函数，返回类型为int型，且main函数的返回必须为int，也就是整数类型（为内置类型，即语言自身定义的类型）；main即为函数名；形参列表为空；函数体包含在这对花括号中；

##### 1.1.1 编译、运行程序

#### 1.2 初始输入、输出

​	c++包含了一个全面的标准库（standard library）来提供**IO**机制。

一个使用**IO**库的程序：

```c++
#include <iostream>
int main()
{
	std::cout << "Enter two numbers:" << std::endl;
	int v1 = 0, v2 = 0;
	std::cin >> v1 >> v2;
	std::cout << "The sum of " << v1 << " and " << v2 << " is " << v1 + v2 << std::endl;

	return 0;
}
```

示例输出：

```c++
Enter two numbers:
4 7
The sum of 4 and 7 is 11
```

​	`#include <iostream>`指出了一个头文件（header），通过使用头文件来链接到标准库，`std::cout << "Enter two numbers:" << std::endl;`执行了一个表达式输出 "" 中的内容，其中（<<）为**输出运算符**，左侧的运算对象必须是一个输出流（ostream），右侧的运算对象是要打印的值；endl 是一个被称为操纵符（manipulator）的特殊值，效果为结束当前行，并将与设备关联的缓冲区（buffer）中的内容刷到设备中；`std::cin >> v1 >> v2;`该语句读入输入数据，**输入运算符**（>>），它接受一个输入流（istream）作为其左侧运算对象，接受一个对象作为其右侧运算对象，它从给定的istream读入数据，存入给定对象中；通过使用`std::endl`的语法来使用命名空间std中的名字，（::）为作用域运算符；

#### 1.3 注释简介

​	注释（comments）可以帮助人类读者理解程序的作用，但是编译器会忽略注释；

单行注释：使用双斜线（//），注释掉该符号右边的所有文本

```c++
// 这是一条注释 ///
```

界定符注释（也就是多行注释）：使用两个界定符（/**/），界定符注释不能嵌套使用；

```c++
/*
*这是
*一条
*多行
*注释
*/
```

#### 1.4 控制流

##### 1.4.1 while语句

​	while语句反复执行一段代码，直到while的条件（condition）为假时为止；

```c++
#include <iostream>
int main()
{
	int sum = 0, val = 0;
	while (val <= 10)
	{
		sum += val;
		++val;
	}
	std::cout << "sum: " << sum << std::endl;
	return 0;
}
```

这段代码中while的条件为`val <= 10`，直到val的值大于10时，while循环推出；这里循环体为花括号包围的两个语句；

##### 1.4.2 for语句

​	第二种循环语句——for语句；

```c++
#include <iostream>
int main()
{
	int sum = 0;
	for (int val = 0; val <= 10; ++val)
	{
		sum += val;
	}
	std::cout << "sum: " << sum << std::endl;
	return 0;
}
```

每个for语句都包含两个部分：循环头和循环体。循环头控制循环体的执行次数，由三部分组成：初始化语句（init-statement）、循环条件（condition）、表达式（expression）；

##### 1.4.3 读取数量不定的输入数据

通过while循环读取数量不定的输入数据，由于`std::cin`输入遇到错误时，istream对象的状态会变为无效可以使条件语句变成假，所以这里使用它作为while循环的条件判断；

```c++
#include <iostream>
int main()
{
	int sum = 0, value = 0;
	while (std::cin >> value)
	{
		sum += value;
	}
	std::cout << "sum: " << sum << std::endl;
	return 0;
}
```

示例结果：这里的^Z为Windows下的文件结束符，使得`std::cin`的istream对象变为无效状态；

```c++
12 45 7 12 99 ^Z
sum: 175
```

##### 1.4.4 if语句

​	使用if语句来支持条件执行，if 右边括号中的为条件；

```c++
#include <iostream>
int main()
{
	int a = 0, b = 0;
	std::cout << "Enter two numbers." << std::endl;
	std::cout << "a:" << std::endl;
	std::cin >> a;
	std::cout << "b:" << std::endl;
	std::cin >> b;
	if (a > b)
	{
		std::cout << "a is bigger!" << std::endl;
	}
	else
	{
		std::cout << "b is bigger!" << std::endl;
	}
	return 0;
}
```

结果示例：

```c++
Enter two numbers.
a:
3
b:
9
b is bigger!
```

#### 1.5 类简介

​	我们通过定义一个类（class）来定义自己的数据结构。一个类定义了一个类型，以及与其关联的一组操作；成员函数（member function）是定义为类的一部分的函数，有时也被称为方法（method）；通常使用`class.method()`的形式来调用成员函数；