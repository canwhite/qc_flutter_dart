# qc_flutter_dart
dart 

## dart

这里讲一下dart的使用，写一个快速入门讲解吧

```
---------------------------------------------------------------------
1）变量
当作js用，var ，const（ 编译监测，直接定义赋值） ，final（运行时，先定义再赋值）
--补充下String、Array和Map
*String
todo

*Array
todo

*Map
todo

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
