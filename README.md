# Programming in Scala第三版学习笔记, 示例代码中文命名

前言: 本书已有中文版, 此笔记并不是对原教程的翻译, 而是围绕示例进行选摘, 并顺便将所有示例改成中文命名(不拘泥于原本命名用词, 而是融入中文特色).

**本文代码在Scala 2.12.4, Java 1.8.0_45下测试通过**

### 第一章 普适的语言

Scala这个名字来源于"scalable语言", 当初的设想是能够用在小到脚本大到系统. Scala在标准Java平台上运行, 可以和Java库无缝集成. 技术上说, 它是一个包含了面向对象和函数式编程概念的静态类型语言, 设计的希望是取众家之长.

这章是简介Scala特性以及它能做什么, 但并不是真正的入门(啥??). 如果希望马上写Scala程序, 还是从第二章开始吧.

#### 1.1 

```scala
var 首都 = Map("中国" -> "北京", "俄罗斯" -> "莫斯科")
首都 += ("德国" -> "柏林")
println(首都("俄罗斯"))
```
(待续. 先从第二章开始)

### 第二章 蹒跚学步

此章将从0开始介绍Scala,为后两章打基础. 看完之后应该能用Scala写实用程序了(好的,那么这个笔记的第一个小目标就是看完前四章)

#### 第一步 
安装了Scala之后,在命令行(控制台)中输入`scala`之后, 就启动了解释器运行环境(理解输入的代码,运行并显示结果):
```
$ scala
Welcome to Scala 2.12.4 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_45).
Type in expressions for evaluation. Or try :help.

scala>
```
试试最简单的加法:
```
scala> 1 + 2
```
解释器打印:
```
res0: Int = 3
```
意思是: res0(自动生成的名称, 就是result 0的简写)是个整数(Int),值为(=)3. 它可以在之后被引用, 比如:
```
scala> res0 * 3
res1: Int = 9
```
不免俗地问个好吧:
```
  scala> println("吃了么?")
  吃了么?
```
println把字符串输出到标准输出(显示屏), 类似Java的System.out.println

#### 第二步 定义变量

有两种, val在定义后就不能被重新赋值, 类似Java中的final. var就可以随便赋值. 例如:
```
scala> val 问话 = "吃了么?"
问话: String = 吃了么?
```
如果习惯了Java中定义变量的方式, 也许会惊讶于为何不用显式声明`String`, 这是因为Scala在这里能自行推导出`问话`是`String`类型. 当然它的推导是很机械的, 有时也不能猜到你想要的类型. 因此也有显式定义类型的方法, 只是格式和Java有点区别:
```
scala> val 又问话: String = "吃了好"
又问话: String = 吃了好
```
定义了`问话`之后,就可以用了:
```
scala> println(问话)
吃了么?
```
问话因为是val,它就不能被重新赋值. 即使赋的是完全相同的值, 解释器也会报错:
```
scala> 问话 = "吃了么?"
<console>:12: error: reassignment to val
       问话 = "吃了么?"
```
如果重新赋值是必要的, 那么就用var, 比如:
```
scala> var 问好 = "早啊"
问好: String = 早啊
```
如果快到吃饭的时候了,问好就可以改成:
```
scala> var 问好 = "吃了么?"
问好: String = 吃了么?
```
如果输入的是多行, 只要换行后继续输入即可. 解释器会自动在接续的行前加`|`:
```
scala> var 多行 =
     | "这是又一行"
多行: String = 这是又一行
```
如果输错了, 而解释器还在等待新输入, 只要换两次行, 解释器就会重新等待新输入:
```
scala> var 放空中 =
     | 
     | 
You typed two blank lines.  Starting a new command.

scala> 
```
在以后的示例中, 将把这些`|`省略,以便阅读, 以及拷贝黏贴到解释器自行运行.

#### 第三步. 定义函数

用过了变量, 不妨来写点函数(这不是最简单的函数):
```
scala> def 最大值(x: Int, y: Int): Int = {
        if (x > y) x
        else y
      }
最大值: (x: Int, y: Int)Int
```
def表示后面的是函数定义, `最大值`是函数名称, `()`内的是函数参数, `: Int`正如之前的变量定义类似, 是表示函数的返回值类型. `{}`包括的是函数体.

和变量定义类似, 有时可以让推导返回值, 就不用声明返回值类型. 如果函数体只有一条声明, 就可以作如下省略:
```
scala> def 最大值(x: Int, y: Int) = if (x > y) x else y
最大值: (x: Int, y: Int)Int
```
定义函数之后, 就可以用了:
```
scala> 最大值(3, 5)
res0: Int = 5
```
下面的函数没有参数也没有返回值:
```
scala> def 问好() = println("吃了么?")
问好: ()Unit
```
Scala中的Unit类型类似于Java中的void. Java中所有的void返回值的方法都对应到返回值是Unit类型的Scala方法.
下面把Scala代码放在文件中运行. `:quit`或者`:q`退出解释器:
```
scala> :q
```

#### 第四步. 写脚本
运行:
```
$ scala 你好.scala
```
用args可以引入命令行参数, 索引从0开始. 运行:
```
$ scala 带参数问好.scala 大黄
```
输出:
```
你好, 大黄
```

#### 第五步. while循环; if条件判断

```scala
var 索引 = 0
while (索引 < args.length) {
  if (索引 != 0) {
    print(" ");
  }
  print(args(索引))
  索引 += 1
}
println()
```
Scala可以省略句尾的分号.

#### 第六步. foreach 和 for

```
args.foreach(参数 => println(参数))
```
效果和前例相同. 只要程序用不着`索引`, 就不用while结构了

如果要显式定义`参数`的类型, 就用`(参数: String)`

如果函数只有一个参数, 就可以进一步简化成这样:
```
  args.foreach(println)
```
for循环的例子:
```
for(参数 <- args)
  println(参数)
```
其中`参数`省略了val, 也就是说它不可以被重新赋值

(第二章完)

### 第三章 上路

此章之后, 应该可以用Scala写有用的脚本了. 不妨动手尝试.

#### 第七步. 带类型的数组

下面初始化一个BigInteger, 并初始化为`12345`
```
var 大数 = new java.math.BigInteger("12345")
```
带类型的数组示例:
```scala
val 问候字段 = new Array[String](3)

问候字段(0) = "你好"
问候字段(1) = ", "
问候字段(2) = "吃了么?\n"

for (索引 <- 0 to 2)
  print(问候字段(索引))
```
上面其实是下面的简写版:
```scala
  val 问候字段 = new Array[String](3)
  
  问候字段.update(0, "你好")
  问候字段.update(1, ", ")
  问候字段.update(2, "吃了么\n")
  
  for (索引 <- 0.to(2))
    print(问候字段.apply(索引))
```
新建数组可以很简单:
```
val 数字 = Array("零", "一", "二")
```
因为初始化使用的是字符串, 因此"数字"理应是字符串数组, 即使没有显式声明

上面代码是下面的简化版. 实际上Array.apply是个静态方法, 可以创建一个数组, 也称为工厂方法.
```
var 数字 = Array.apply("零", "一", "二")
```

#### 第八步. 列表
Scala中的列表scala.List是不可变的. 而java.util.List是可变的.

下面是创建列表:
```scala
val 一二三 = List(1, 2, 3)
```
因为它的内容是不可变的, 因此很多看似会改变列表的方法, 实际上是新建了一个列表. 比如`:::`是合并列表:
```scala
  val 一二 = List(1, 2)
  val 三四 = List(3, 4)
  val 一二三四 = 一二 ::: 三四
  println(一二 + " 和 " + 三四 + " 没有改变.")
  println("所以, " + 一二三四 + " 是新列表.")
```
会返回:
```
List(1, 2) 和 List(3, 4) 没有改变.
所以, List(1, 2, 3, 4) 是新列表.
```
也许最常用的列表操作符会是`::`, 就是`加塞`, 可以把一个元素加到一个列表的头上, 返回一个新列表.
```scala
val 二三 = List(2, 3)
val 一二三 = 1 :: 二三
```
将会看到`List(1,2,3)`
这里需要说明, 操作符只要末尾有`:`, 它就是作用在它右边的操作数上; 否则作用在左边的操作数.
比如`a * b`, 就是`a.*(b)`(*就是个方法名), 而`1 :: 二三`就是`二三.::(1)`

Nil是空列表, 因此初始化也可以挨个加塞元素, 比如:
```
val 一二三 = 1 :: 2 :: 3 :: Nil
```
取列表元素和数组一样, 也是用(i)

在列表后追加元素可以用`:+`, 但很少用, 因为它的耗时随列表长度线性增加. 而`::`耗时是恒定的. 如果想要以追加元素的方式创建列表, 那么就用`::`, 再调用`reverse`. 同样是创建列表, 前者耗时是O(N^2), 后者是O(N).
列表的内置方法有很多. 详见文档. 十六章将介绍更多列表功能.

#### 第九步 使用元组

元组(Tuple)比列表更加灵活, 因为它允许存放多种类型的数据. 比如:
```scala
val 对 = (99, "久久")
println(对._1)
println(对._2)
```
它会打印第一个和第二个元素. 元组的类型取决于长度和元素类型, 比如"对"的类型是Tuple2(Int, String). 不像列表注意元组的索引开始于1, 因为其他语言(Haskell/ML)中的元组也是如此).

#### 第十步 使用集合(Set)和映射(Map)
**(这里开始仅包含例程与极简说明, 如有空再补详细说明)**

不可变集合
```scala
var 客机厂商 = Set("空客", "波音")
客机厂商 += "商飞"
println(客机厂商.contains("大疆"))
```
可变集合
```scala
import scala.collection.mutable

val 电影 = mutable.Set("舌尖一", "舌尖二")
电影 += "舌尖三"
println(电影)
```
如需指定使用HashSet, 就`import scala.collection.immutable.HashSet`

可变映射
```scala
import scala.collection.mutable

val 寻宝指南 = mutable.Map[Int, String]()
寻宝指南 += (1 -> "上荒岛")
寻宝指南 += (2 -> "在地上找个那啥")
寻宝指南 += (3 -> "开挖")
println(寻宝指南(2))
```

不变映射
```scala
val 中文数字 = Map(1 -> "一", 2 -> "二", 3 -> "三", 4 -> "四", 5 -> "五")
println(中文数字(4))
```

#### 第十一步 学习函数风格
改自第二章例子:
```scala
def 打印参数(参数: Array[String]): Unit = {
  var i = 0
  while (i < 参数.length) {
    println(参数(i))
    i += 1
  }
}
```
如下可以省去var
```scala
def 打印参数(参数: Array[String]): Unit = {
  for (某参数 <- 参数)
    println(某参数)
}
```
或更简单:
```scala
def 打印参数(参数: Array[String]): Unit = {
  参数.foreach(println)
}
```
函数返回类型为Unit就是有副作用的迹象, 下面是无副作用的函数(不打印输出, 也没有var):
```scala
def 格式化参数(参数: Array[String]) = 参数.mkString("\n")
```

用`assert`测试:
```scala
val 结果 = 格式化参数(Array("一", "二", "三"))
assert(结果 == "一\n二\n三")
```
更多测试相关见14章

#### 第十二步 从文件读行
```scala
import scala.io.Source

// 下面"args"如改写为"参数"后报错: error: not found: value 参数
if (args.length > 0) {
  for (行 <- Source.fromFile(args(0)).getLines())
    println(行.length + " " + 行)
}
else
  Console.err.println("请输入文件名")
```
运行`scala 统计字符1.scala  统计字符1.scala`后输出:
```
22 import scala.io.Source
0
50 // 下面"args"如改写为"参数"后报错: error: not found: value 参数
22 if (args.length > 0) {
48   for (行 <- Source.fromFile(args(0)).getLines())
31     println(行.length + " " + 行)
1 }
4 else
31   Console.err.println("请输入文件名")
```
如想输出更漂亮, 下面是最终版:
```scala
import scala.io.Source

def 字符数宽度(文本: String) = 文本.length.toString.length

if (args.length > 0) {
  val 行 = Source.fromFile(args(0)).getLines().toList
  val 最长行 = 行.reduceLeft(
    (行1, 行2) => if (行1.length > 行2.length) 行1 else 行2
  )
  val 最大宽度 = 字符数宽度(最长行)
  for (某行 <- 行) {
    val 空格数 = 最大宽度 - 字符数宽度(某行)
    val 缩进 = " " * 空格数
    println(缩进 + 某行.length + " | " + 某行)
  }
}
else
  Console.err.println("请输入文件名")
```
运行`scala 统计字符2.scala  统计字符2.scala`输出如下:
```
22 | import scala.io.Source
 0 |
49 | def 字符数宽度(文本: String) = 文本.length.toString.length
 0 |
22 | if (args.length > 0) {
52 |   val 行 = Source.fromFile(args(0)).getLines().toList
25 |   val 最长行 = 行.reduceLeft(
53 |     (行1, 行2) => if (行1.length > 行2.length) 行1 else 行2
 3 |   )
23 |   val 最大宽度 = 字符数宽度(最长行)
17 |   for (某行 <- 行) {
30 |     val 空格数 = 最大宽度 - 字符数宽度(某行)
22 |     val 缩进 = " " * 空格数
40 |     println(缩进 + 某行.length + " | " + 某行)
 3 |   }
 1 | }
 4 | else
31 |   Console.err.println("请输入文件名")
```

(第三章完)

### 第四章 类和对象

#### 4.1 类, 变量, 方法

```scala
class 校验累加器 {
}
```
`new 校验累加器`创建对象

添加变量
```scala
class 校验累加器 {
  var 和 = 0
}
```
两个对象
```scala
val 累加器 = new 校验累加器
val 保留进位加法器 = new 校验累加器
```
可以置变量:
```scala
累加器.和 = 3
```
由于`累加器`为val, 不能重赋值如下, 会编译出错
```scala
累加器 = new 校验累加器
```
如果在`var 和`前加`private`, 与Java的`private`相同, 在类外部访问此变量将编译出错. 可以内部访问:
```scala
class 校验累加器 {
  private var 和 = 0

  def 加(值: Byte): Unit = {
    和 += 值
  }

  def 校验(): Int = {
    return ~(和 & 0xFF) + 1
  }
}
```
方法参数不可赋值, 如在`加`方法中, `b = 1`会编译出错

方法可以简写如下:
```scala
class 校验累加器 {
  private var 和 = 0
  def 加(值: Byte) = 和 += 值
  def 校验() = ~(和 & 0xFF) + 1
}
```
虽然编译器可以推导方法类型, 为可读性考虑, 最好写出方法返回类型:
```scala
class 校验累加器 {
  private var 和 = 0
  def 加(值: Byte): Unit = { 和 += 值 }
  def 校验(): Int = ~(和 & 0xFF) + 1
}
```

#### 4.2 分号

一行中多个声明需用分号分隔. 否则末尾可以省略
```scala
val 文本 = "你好"; println(文本)
```

下面两行会被分隔为`x`和`+y`两个声明:
```scala
x
+y
```
如果需要表示`x+y`, 则用括号或将中缀运算符`+`置于末尾:
```scala
x +
y
```

下面几种情况不会被识别为省略分号:
- 行尾词不可能为声明的结尾, 如句号或中缀运算符
- 下一行第一个词不可能为声明开头
- 行结束在括号()或[]的中间, 因为其中不可能有多个声明

#### 4.3 单例对象

用`object`代替`class`, 就成了单例对象. 如果与类名相同, 称为伴随对象, 可以与类互访私有变量:
```scala
// 在文件"校验累加器.scala"中
import scala.collection.mutable

object 校验累加器 {
  private val 缓存 = mutable.Map.empty[String, Int]

  def 计算(文本: String): Int =
    if (缓存.contains(文本))
      缓存(文本)
    else {
      val 累加器 = new 校验累加器
      for (字符 <- 文本)
        累加器.加(字符.toByte)
      val 校验码 = 累加器.校验()
      缓存 += (文本 -> 校验码)
      校验码
    }
}
```
与类比较, 单例对象不能传入参数. 如果没有伴随类, 仅有单例对象, 不能创建`校验累加器`类型的对象. 单例对象可用于功用方法或应用入口(见下节)

#### 4.4 一个Scala应用

建议文件名与包含类名相同
```scala
// 夏季.scala
import 校验累加器.计算

object 夏季 {
  def main(参数: Array[String]) = {
    for (某参数 <- 参数)
      println(某参数 + ": " + 计算(某参数))
  }
}
```
运行`fsc 校验累加器.scala 夏季.scala`进行编译后运行:
```
$ scala 夏季 的 浪漫
的: -132
浪漫: -149
```

#### 4.5 App接口

```scala
import 校验累加器.计算

object 春夏秋冬 extends App {
  for (季节 <- List("秋", "冬", "春"))
    println(季节 + ": " + 计算(季节))
}
```
运行`fsc 春夏秋冬.scala`后运行如下:
```
$ scala 春夏秋冬
秋: -203
冬: -172
春: -37
```

### 发现的中文相关问题
命令行交互环境中, 错误信息对中文字符的定位不准. 这很干扰排错. 比较如下两个同样出错信息:
```
scala> println(["2"])
<console>:1: error: illegal start of simple expression
       println(["2"])
               ^

scala> 打印参数(["2"])
<console>:1: error: illegal start of simple expression
       打印参数(["2"])
            ^
```