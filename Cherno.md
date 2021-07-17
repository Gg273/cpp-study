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

C++库中有一种内置数据结构叫做标准数组，它具有边界检查，跟踪数组大小等优势所在；使用这个标准数组需要包含头文件`#include <array>`；

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