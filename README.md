#什么是Kotlin？
![图片发自简书App](http://upload-images.jianshu.io/upload_images/1672313-5157dedd9381deb2.JPG)



**Kotlin是JetBrains开发的基于JVM的语言，JetBrains想必大家应该很熟悉了，他们创造了很多强大的IDE，android studio谷歌官方的android IDE就是基于Intellij，kotlin可以作为一个插件被用来开发android跟java比kotlin有什么好处？**
**1.它更容易表现**，使用kotlin你可以少写很多代码，比如创建数据类等。
**2.它更安全**，在用Java开发时，大多数代码都是预防性的。为了不遇到非预期的NullPointerException，在使用之前，要不断的检测对象是否为空。与许多其它语言一样，因为需要使用安全调用运算符显式指明对象是否能够为空（null），所以Kotlin是空类型安全的
**3.它是函数式的**，Kotlin是基于面向对象的语言。但是就如其他很多现代的语言那样，它使用了很多函数式编程的概念，比如，使用lambda表达式来更方便地解决问题。其中一个很棒的特性就是Collections的处理方式。
**4.它可以扩展函数**，这意味着我们可以扩展类的更多的特性，甚至我们没有权限去访问这个类
>[kotlin官方文档传送门：https://kotlinlang.org/docs/reference/basic-syntax.html](https://kotlinlang.org/docs/reference/basic-syntax.html)

#1.入门
##1.1 基本语法
###1.1.1 定义包
包说明应该在源文件的顶部：
```
package my.demo
import java.util.*
// ...
```
*不要求包与目录匹配：源文件可以在系统中的任意地方。 

###1.12 定义函数
函数带有两个int类型参数，并且返回int类型值：
```
fun sum(a: Int, b: Int): Int { 
return a + b
}
```
函数体可以是个表达式，并可以从中推断出返回值类型：
```
fun sum(a: Int, b: Int) = a + b
```
函数也可以返回无意义的值：
```
fun printSum(a: Int, b: Int): Unit {
 print(a + b)
}
```
Unit返回值类型可以省略：
```
fun printSum(a: Int, b: Int) { 
print(a + b)
}
```
###1.1.3 定义局部变量
一次赋值（只读）局部变量：
```
val a: Int = 1
val b = 1 //  推断为Int类型 
val c: Int  // 如果没有初始化就要求说明类型
c = 1 // 明确赋值
```
可变变量：
```
var x = 5 // 推断为Int类型 
x += 1
```
>######提示
就像 Java 和 JavaScript, Kotlin 支持以下两种代码注释方式：
```
// This is an end-of-line comment
/* This is a block comment on multiple lines. */
```

###1.1.4 使用字符串模板
```
fun main(args: Array<String>) {
 if (args.size == 0) return 
print("First argument: ${args[0]}")}
```
### 1.1.5 使用条件表达式
```
fun max(a: Int, b: Int): Int {
 if (a > b) 
     return a 
else
     return b
}
```
使用if表达式：
```
fun max(a: Int, b: Int) = if (a > b) a else b
```
###1.1.6使用nullable值检测空（null）值
当空值可能出现时，引用必须明确标记出可null值。
如果str没有保存一个整数，则返回null：
```
fun parseInt(str: String): Int? { 
    // ...
}
```
用函数返回可null值：
```
fun main(args: Array<String>) {   
   if (args.size < 2) {       
     print("Two integers expected")    
     return  
  }  
 val x = parseInt(args[0])   
 val y = parseInt(args[1])   

 //  由于x，y是null，所以使用x*y将产生错误。
  if (x != null && y != null) {      
     // 在null检查后，x和y自动地配置（cast）到非可空      
     print(x * y)  
  }
}
```
或
```
// ...
if (x == null) { 
    print("Wrong number format in '${args[0]}'") 
    return 
}
if (y == null) { 
    print("Wrong number format in '${args[1]}'")
    return 
} 

// 在空检查后，x和y自动的匹配到非可null
print(x * y)
```
### 1.1.7  使用类型检查和自动类型转换
is操作符检查表达式是否类型实例。如果对不可变局部的变量或属性进行特定类型检查了，就不需要明确的类型转换。
```
fun getStringLength(obj: Any): Int? { 
if (obj is String) { 
// 在这个分支中，`obj`自动转换到`String`
   return obj.length 
} 
// 在类型检查分支之外，`obj`仍然是`Any`类型
   return null
}
```
或
```
fun getStringLength(obj: Any): Int? {
  if (obj !is String)
    return null

  // 在这个分支上，`obj`自动转换到`String`
  return obj.length
}
```
甚至
```
fun getStringLength(obj: Any): Int? {
  // 在`&&`右手边条件成立时，`obj`自动转换到`String`
  if (obj is String && obj.length > 0)
    return obj.length

  return null
}
```
### 1.1.8 使用for循环
```
fun main(args: Array<String>) {
   for (arg in args)
     print(arg) 
}
```
或
```
for (i in args.indices) 
   print(args[i])
```
### 1.1.9 使用while循环
```
fun main(args: Array<String>) { 
  var i = 0 
  while (i < args.size) 
      print(args[i++])
}
```
### 1.1.10 使用when表达式
```
fun cases(obj: Any) {
  when (obj) {
    1                -> print("One")
    "Hello"        -> print("Greeting")
    is Long       -> print("Long")
    !is String     -> print("Not a string")
    else             -> print("Unknown")
  }
}
```
### 1.1.11 使用范围
使用in操作符检查一个数字是否在一个范围内：
```
if (x in 1..y-1) 
  print("OK")
```
检查一个数字是否超出范围：
```
if (x !in 0..array.lastIndex) 
  print("Out")
```
遍历整个范围：
```
for (x in 1..5) 
   print(x)
```
###1.1.12 使用集合
遍历一个集合：
```
for (name in names) 
   println(name)
```
使用in操作符检查一个集合是否包含一个对象：
```
if (text in names) // 调用names.contains(text)
  print("Yes")
```
使用Lambda表达式过滤和映射集合：
```
names 
         .filter { it.startsWith("A") } 
         .sortedBy { it } 
         .map { it.toUpperCase() } 
         .forEach { print(it) }
```
##1.2 习惯用语
这里随机收集了一些经常在Kotlin中使用的习惯用语，如果你有喜欢的，也可以贡献出来，和我们的合并。
###1.21 创建DTO（POJO/POCO）
```
data class Customer(val name: String, val email: String)
```
提供带有下列功能的Customer类：
  -所有属性的getter（和var的setter）
  -equals()
  -hashCode()
  -toString()
  -copy()
  -component1()，component2()
### 1.2.2 函数参数的默认值
```
fun foo(a: Int = 0, b: String = "") { ... }
```
### 1.2.3 过滤列表
```
val positives = list.filter { x -> x > 0 }
```
或者更简洁的写法：
```
val positives = list.filter { it > 0 }
```
### 1.2.4 字符串插值
```
println("Name $name")
```
### 1.2.5 实例检查
```
when (x) {
    is Foo -> ... 
    is Bar -> ... 
    else -> ...}
```
### 1.2.6 遍历键值对/列表对
```
for ((k, v) in map) {
   println("$k -> $v")
}
```
k,v可以调用任何东西。
###1.2.7  使用范围
```
for (i in 1..100) { ... }
for (x in 2..10) { ... }
```
###1.2.8 只读列表
```
val list = listOf("a", "b", "c")
```
###1.2.9 只读映键值对
```
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
```
###1.2.10 访问键值对
```
println(map["key"])
map["key"] = value
```
###1.2.11 Lazy属性
```
val p: String by lazy {
 // 计算串
}
```
###1.2.12 扩展函数
```
fun String.spaceToCamelCase() { ... }"

Convert this to camelcase".spaceToCamelCase()
```
###1.2.13 创建单例模式
```
object Resource { 
    val name = "Name"
}
```
###1.2.14 if非空简写
```
val files = File("Test").listFiles()

println(files?.size)
```
>未完
>如有不足，纯属作者太菜，请大家多多指点
