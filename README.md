# qc_flutter_dart
dart 

## dart

这里讲一下dart的使用，写一个快速入门讲解吧

```
---------------------------------------------------------------------
1）变量
当作js用，var ，const（ 编译监测，直接定义赋值） ，final（运行时，先定义再赋值）
--补充下String、Array和Map

*数据类型
数字类型（Number Types）：

int：表示整数值，例如 42。
double：表示双精度浮点数，例如 3.14。
布尔类型（Boolean Type）：

bool：表示布尔值，只有两个取值：true 和 false。
字符串类型（String Type）：

String：表示一系列字符组成的字符串，例如 'Hello' 或 "Dart"。
列表类型（List Type）：

List：表示有序的集合，可以包含任意类型的元素。例如 [1, 2, 3] 或 ['apple', 'banana', 'orange']。
映射类型（Map Type）：

Map：表示键值对的集合，可以将键映射到值。例如 {'name': 'Alice', 'age': 25}。
集合类型（Set Type）：

Set：表示无序的唯一元素集合。例如 {1, 2, 3}。
符号类型（Symbol Type）：

Symbol：表示 Dart 程序中的符号。符号是 Dart 运行时系统使用的特殊对象。
空类型（Null Type）：

Null：表示一个空值，即没有引用任何对象。


--着重讲以下几个
*String

String greeting = 'Hello';
String name = 'Alice';
String message = greeting + ', ' + name + '!'; // 字符串拼接
print(message); // 输出：Hello, Alice!

String substring = message.substring(7); // 获取子字符串
print(substring); // 输出：Alice!

String replaced = message.replaceAll('Alice', 'Bob'); // 字符串替换
print(replaced); // 输出：Hello, Bob!


*List

List<int> numbers = [1, 2, 3, 4, 5];
numbers.add(6); // 添加元素
print(numbers); // 输出：[1, 2, 3, 4, 5, 6]

numbers.removeAt(2); // 移除指定索引处的元素
print(numbers); // 输出：[1, 2, 4, 5]

int length = numbers.length; // 获取数组长度
print(length); // 输出：4



*Map

Map<String, int> scores = {
  'Alice': 95,
  'Bob': 80,
  'Charlie': 90,
};

scores['David'] = 88; // 添加键值对
print(scores); // 输出：{Alice: 95, Bob: 80, Charlie: 90, David: 88}

scores.remove('Bob'); // 移除指定键的键值对
print(scores); // 输出：{Alice: 95, Charlie: 90}

List<String> keys = scores.keys.toList(); // 获取键的列表
print(keys); // 输出：[Alice, Charlie]

List<int> values = scores.values.toList(); // 获取值的列表
print(values); // 输出：[95, 90]


---------------------------------------------------------------------
2）if/for - 可以当js用
* 常规款
* forEach款
numbers.forEach((item) {
  print(item); 
});


---------------------------------------------------------------------
3）function和callback -当java使用

//callback
void callbackFunc(Function func) {
  func(); 
}
 
void printMsg() {
  print('Called printMsg()!');
}
callbackFunc(printMsg);



---------------------------------------------------------------------
4）export/import

Dart 的widgets 不需要单独 export 出去。
Dart/Flutter 的库(library)有一个隐式的根export,也就是说所有定义在该库中的内容默认已经"export"出去了,可以直接从其他文件import使用。


//以下是方法
import 'package:flutter/material.dart';
import '../pages/details.dart';


export 'index.dart' show getRouters;
Map<String, WidgetBuilder> getRouters(BuildContext context) {
    final Map<String, WidgetBuilder> routers = {

        //page1
        '/detail': (context) => DetailPage(),
        
        //page2...

        //page3...
    };
    return routers;
}



---------------------------------------------------------------------
5）class and inheritance


class Spacecraft {
  String name;
  DateTime? launchDate;


  // Read-only non-final property
  int? get launchYear => launchDate?.year;


  // Constructor, with syntactic sugar for assignment to members.
  Spacecraft(this.name, this.launchDate) {
    // Initialization code goes here.
  }


  // Named constructor that forwards to the default one.
  Spacecraft.unlaunched(String name) : this(name, null);


  // Method.
  void describe() {
    print('Spacecraft: $name');
    // Type promotion doesn't work on getters.
    var launchDate = this.launchDate;
    if (launchDate != null) {
      int years = DateTime.now().difference(launchDate).inDays ~/ 365;
      print('Launched: $launchYear ($years years ago)');
    } else {
      print('Unlaunched');
    }
  }
}



//继承很有意思
class Orbiter extends Spacecraft {
// Named constructor，前边的是自己的，可以在{}中展开，后边的是继承的，用:隔开，这算是语法糖
//const MyHomePage({Key? key, required this.title, required this.context})
: super(key: key);

  
  double altitude;
  Orbiter(super.name, DateTime super.launchDate, this.altitude);
}


还有Mixin和java有些不同，其余interface和abstract和java基本一样
MiXIn需要再后边用with继承

mixin Piloted {
  int astronauts = 1;


  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}

//mixin插入的值和方法可以直接调用
class PilotedCraft extends Spacecraft with Piloted {
  // ···
}

---------------------------------------------------------------------
Future<int> fetchData() async {
  // 模拟异步操作，例如从网络或数据库获取数据
  await Future.delayed(Duration(seconds: 2));

  // 返回异步操作的结果
  return 42;
}
void main() async {
  int result = await fetchData();
  print(result); // 打印异步操作的结果
}

or:
void main() {
  fetchData().then((result) {
    print(result); // 打印异步操作的结果
  });
}


```
