

```scala
import scala.collection.mutable._
```


```scala
object Demo01 {
    println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
    //--声明一个变量,变量声明之后,可以修改值
    var v1=100                                      //> v1  : Int = 100
    v1=200
    //--声明一个常量,常量一经声明,不允许修改
    val v2="hello"                                  //> v2  : String = hello
    val v3="world" ;val v4="scala"            //> v3  : String = world
                                                      //| v4  : String = scala
    val v5:String="hello"                     //> v5  : String = hello
    val v6=Array(1,2,3,4)                     //> v6  : Array[Int] = Array(1, 2, 3, 4)
    val v8=Array("hello","world")             //> v8  : Array[String] = Array(hello, world)
}
```


    defined object Demo01
    



```scala
object Demo02 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  val s1="hello world"                            //> s1  : String = hello world
  val r1=s1.split(" ")                            //> r1  : Array[String] = Array(hello, world)
  //--取出前n个元素并返回
  val r2=s1.take(5)                               //> r2  : String = hello
  //--取出尾部n个元素并返回
  val r3=s1.takeRight(5)                          //> r3  : String = world
  //--去掉前n个元素,并返回剩余元素
  val r4=s1.drop(2)                               //> r4  : String = llo world
  //--去掉尾部n个元素,并返回剩余元素
  val r5=s1.dropRight(2)                          //> r5  : String = hello wor
  //--重复n次
  val r6=s1*2                                     //> r6  : String = hello worldhello world
  //--去重
  val r7=s1.distinct                              //> r7  : String = helo wrd
  //--反转
  val r8=s1.reverse                               //> r8  : String = dlrow olleh  
  val s2="100"                                    //> s2  : String = 100
  //--类型转换
  val r9=s2.toInt                                 //> r9  : Int = 100
  val r10=s2.toDouble                             //> r10  : Double = 100.0
}
```


    defined object Demo02
    



```scala
object Demo03 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  val i1=1                                        //> i1  : Int = 1
  //--用于生成区间,一般用于循环遍历时,生成范围
  val r1=i1.to(5)                                 //> r1  : scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5)
  //--生成区间,并指定步长
  val r2=i1.to(5,2)                               //> r2  : scala.collection.immutable.Range.Inclusive = Range(1, 3, 5)
  //--生成区间,不含尾元素		       //> r3  : scala.collection.immutable.Range = Range(1, 2, 3, 4)
  val r3=i1.until(5)                              //> r4  : scala.collection.immutable.Range = Range(1, 3)
  val r4=i1.until(5,2) 
  val r5=1+3*2                                    //> r5  : Int = 7
  val r6=1.+(3).*(2)                              //> r6  : Int = 8
  //--scala有4种前缀操作符,需要加空格
  //--正数
  val i2= +2                                      //> i2  : Int = 2
  //--负数
  val i3= -2                                      //> i3  : Int = -2
  //--布尔取反
  val i4= !true                                   //> i4  : Boolean = false
  //--二进制取反
  val i5= ~0XFF                                   //> i5  : Int = -256
  //--避免出现歧义,也可以用下面的方式表示
  val i6=2.unary_+                                //> i6  : Int = 2
  val i7=2.unary_-                                //> i7  : Int = -2
  val i8=true.unary_!                             //> i8  : Boolean = false
  val i9=0XFF.unary_~                             //> i9  : Int = -256
}
```


    defined object Demo03
    



```scala
object Demo04 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  val i1=3                                        //> i1  : Int = 3
  val r1=if(i1>5)println("big") else println("small")
                                                  //> small
                                                  //| r1  : Unit = ()
  val a1=Array(1,2,3,4)                           //> a1  : Array[Int] = Array(1, 2, 3, 4)
  var index=0                                     //> index  : Int = 0
  while(index<a1.length){
  println(a1(index))
  index+=1
  }                                               //> 1
                                                  //| 2
                                                  //| 3
                                                  //| 4
}
```


    defined object Demo04
    



```scala
object Demo05 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  val a1=Array(1,2,3,4)                           //> a1  : Array[Int] = Array(1, 2, 3, 4)
  for(i<-a1){
  println(i)
}
  //val a2=1.to(10)
  val a2=1 to 10                                  //> a2  : scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5, 6, 7
                                                  //| , 8, 9, 10)
  for(i<-a2){
  println(i)                                      
}
  //--scala支持在for(写条件语句)
  for(i<-1 to 10;if i>6&&i%2==0){
  println(i)                                      
}
 for(i<-1 to 10;if i>6;if i%2==0) println(i)     //> 8
                                                  //| 10
}
```


    defined object Demo05
    



```scala
for(a<-1 to 9){
  
  for(b<-1 to a){
  print(b+"*"+a+"="+b*a+"\t")
  }
  println()
}
```

    1*1=1	
    1*2=2	2*2=4	
    1*3=3	2*3=6	3*3=9	
    1*4=4	2*4=8	3*4=12	4*4=16	
    1*5=5	2*5=10	3*5=15	4*5=20	5*5=25	
    1*6=6	2*6=12	3*6=18	4*6=24	5*6=30	6*6=36	
    1*7=7	2*7=14	3*7=21	4*7=28	5*7=35	6*7=42	7*7=49	
    1*8=8	2*8=16	3*8=24	4*8=32	5*8=40	6*8=48	7*8=56	8*8=64	
    1*9=9	2*9=18	3*9=27	4*9=36	5*9=45	6*9=54	7*9=63	8*9=72	9*9=81	
    


```scala
for(a<-1 to 9;b<-1 to a;val sep=if(b==a)"\r\n" else "\t")print(b+"*"+a+"="+b*a+sep)
```


    warning: there was one deprecation warning; re-run with -deprecation for details
    


    1*1=1
    1*2=2	2*2=4
    1*3=3	2*3=6	3*3=9
    1*4=4	2*4=8	3*4=12	4*4=16
    1*5=5	2*5=10	3*5=15	4*5=20	5*5=25
    1*6=6	2*6=12	3*6=18	4*6=24	5*6=30	6*6=36
    1*7=7	2*7=14	3*7=21	4*7=28	5*7=35	6*7=42	7*7=49
    1*8=8	2*8=16	3*8=24	4*8=32	5*8=40	6*8=48	7*8=56	8*8=64
    1*9=9	2*9=18	3*9=27	4*9=36	5*9=45	6*9=54	7*9=63	8*9=72	9*9=81
    


```scala
for(a<-1 to 9;b<-1 to a;val sep=if(b==a)"\r\n" else "\t"){
   print(s"$b*$a=${b*a}$sep") 
}
```


    warning: there was one deprecation warning; re-run with -deprecation for details
    


    1*1=1
    1*2=2	2*2=4
    1*3=3	2*3=6	3*3=9
    1*4=4	2*4=8	3*4=12	4*4=16
    1*5=5	2*5=10	3*5=15	4*5=20	5*5=25
    1*6=6	2*6=12	3*6=18	4*6=24	5*6=30	6*6=36
    1*7=7	2*7=14	3*7=21	4*7=28	5*7=35	6*7=42	7*7=49
    1*8=8	2*8=16	3*8=24	4*8=32	5*8=40	6*8=48	7*8=56	8*8=64
    1*9=9	2*9=18	3*9=27	4*9=36	5*9=45	6*9=54	7*9=63	8*9=72	9*9=81
    


```scala
//--声明一个map(key->value)
val m1=Map("tom"->23,"rose"->30,"tom"->35)//> m1  : scala.collection.immutable.Map[String,Int] = Map(tom -> 35, rose -> 30
```


    m1 = Map(rose -> 30, tom -> 35)
    





    Map(rose -> 30, tom -> 35)




```scala
m1("tom")                                 //> res0: Int = 35
```




    35




```scala
for(i<-m1){ println(i)}
```

    (rose,30)
    (tom,35)
    


```scala
//--掌握这种遍历map的方式
for((k,v)<-m1){ println(v)}
val a3=Array(1,2,3,4)                     //> a3  : Array[Int] = Array(1, 2, 3, 4)
val a4=for(i<-a3)yield{i*2}               //> a4  : Array[Int] = Array(2, 4, 6, 8)
val l1=List(1,2,3,4)                      //> l1  : List[Int] = List(1, 2, 3, 4)
val l2=for(i<-l1)yield{i*3}               //> l2  : List[Int] = List(3, 6, 9, 12)
```

    30
    35
    


    a3 = Array(1, 2, 3, 4)
    a4 = Array(2, 4, 6, 8)
    l1 = List(1, 2, 3, 4)
    l2 = List(3, 6, 9, 12)
    





    List(3, 6, 9, 12)




```scala
import util.control.Breaks._
object Demo07 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  //--把循环写在breakable()里,此时的break是跳出循环效果
  breakable(
  for(i<-1 to 10){
  if(i>8){  break
  }else{  println(i)
  }
   }
  )
//--把循环卸载breakable()外,此时的break是continue效果
  for(i<-1 to 10){
  breakable(
  if(i==8){
  break
  }else{
  println(i)
  }
  )                                               //> 1
}
}
```


    defined object Demo07
    



```scala
object Demo01 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  for(i<-1 to 10 reverse)println(i) 
  for(i<-10 to 1 by -1)println(i) 
  val m1=Map("book"->10,"gun"->100,"ipad"->1000)   //> m1  : scala.collection.immutable.Map[String,Int] = Map(book -> 10, gun -> 10
                                                  //| 0, ipad -> 1000)
  val m2=for((k,v)<-m1)yield{(k,v*0.9)}            //> m2  : scala.collection.immutable.Map[String,Double] = Map(book -> 9.0, gun -
                                                  //| > 90.0, ipad -> 900.0)
}
```


    defined object Demo01
    



    warning: there was one feature warning; re-run with -feature for details
    



```scala
object Demo02 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  def f1():String={
    "hello1811"
  }                                               //> f1: ()String
  def f2()={
  "hello1811"
  }                                               //> f2: ()String
  def f3()={
  Array(1,2,3,4)
  }                                               //> f3: ()Array[Int]
  def f4()={
    }                                               //> f4: ()Unit
  def f5(){
  "hello1811"
  }                                               //> f5: ()Unit
  def f6(a:Int,b:Int)={
  a+b
  }                                               //> f6: (a: Int, b: Int)Int
  f6(2,3)                                         //> res0: Int = 5
  //--定义f7函数,接收一个字符串,方法体中按,切割字符串
  def f7(a:String):Array[String]={
  a.split(",")
  }                                               //> f7: (a: String)Array[String]
  f7("hello,world")                               //> res1: Array[String] = Array(hello, world)
  //--定义一个f8函数,接收一个整型数组,方法体中遍历数组打印
  def f8(a:Array[Int])={
  for(i<-a)println(i)
  }                                               //> f8: (a: Array[Int])Unit
  f8(Array(1,2,3,4))                              //> 1
                                                  //| 2
                                                  //| 3
                                                  //| 4
  //--scala的默认参数机制,可以在声明函数时,为参数指定默认值
 def f9(a:String,b:String="*",c:String="&")={
 b+a+c
 }                                         //> f9: (a: String, b: String, c: String)String
 f9("hello")                               //> res2: String = *hello&
 f9("hello","#")                           //> res3: String = #hello&
 //--scala的变长参数机制,在类型后面加*
 //--变长参数类型本质是集合类型,可以通过集合的方法来操作
 def f10(a:Int*)={
 for(i<-a)println(i)
 }                                         //> f10: (a: Int*)Unit
 f10(2,3,4,5)                              //> 2
                                                  //| 3
                                                  //| 4
                                                  //| 5
  //--变长参数类型必须位于参数列表最后
 def f11(b:Int,a:String*)={
 }                                         //> f11: (b: Int, a: String*)Unit
}
```


    defined object Demo02
    



    <console>:48: warning: a pure expression does nothing in statement position; you may be omitting necessary parentheses
      "hello1811"
      ^
    



```scala
class Person {
  //--函数定义在类的内部,则此函数是类的成员函数
  def eat()={
    println("eat food")
    //--定义在函数内的函数称为本地函数
    //--本地函数不能通过对象来调用
    def cook()={
      println("cook")
    }
  }
}
```


    defined class Person
    



```scala
val p1=new Person                         //> p1  : Person = Person@3498ed
p1.eat()                                  //> eat food
```

    eat food
    


    p1 = Person@58031243
    





    Person@58031243




```scala
object Demo16 {
  class Student{
    def eat(food:String){
      //cook函数内嵌在eat函数里，这样的函数称之为本地函数
      def cook(food:String):String={
        "做熟了的"+food;
      }
      println("吃"+cook(food));
    }
  }
    
  def main(args: Array[String]): Unit = {
    val p=new Student();
    p.eat("肉");
  }
}
```


    defined object Demo16
    



```scala
object Demo03 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  
  def f1(a:Int,b:Int)={a+b}                       //> f1: (a: Int, b: Int)Int
  
  //--声明一个匿名函数    //--将匿名函数当做参数赋值
  val f2=(a:Int,b:Int)=>{a+b}                     //> f2  : (Int, Int) => Int = <function2>
  
  f2(2,3)                                         //> res0: Int = 5
  
  //--将匿名函数当做参数传递
  //--如果一个函数可以将匿名函数当做参数传递,则此函数称为高阶函数
  //--即f3是一个高阶函数,可以把函数当做参数传递
  def f3(a:Int,b:Int,f:(Int,Int)=>Int)={
  f(a,b)
  }                                               //> f3: (a: Int, b: Int, f: (Int, Int) => Int)Int
  
  //--调用f3,传入两个整型和一个匿名函数,要求实现两个数乘法运算
  
  f3(2,3,(a:Int,b:Int)=>{a*b})                    //> res1: Int = 6
  f3(2,3,(a,b)=>{a*b})                            //> res2: Int = 6
  f3(2,3,(a,b)=>a*b)                              //> res3: Int = 6
  f3(2,3,_*_)                                     //> res4: Int = 6
  
  
  def f4(a:String,f:(String)=>Array[String])={
  f(a)
  }                                               //> f4: (a: String, f: String => Array[String])Array[String]
  //--根据下面的调用,把f4函数声明出来
  f4("hello,world",(a:String)=>{a.split(",")})    //> res5: Array[String] = Array(hello, world)
  f4("hello,world",(a)=>a.split(","))             //> res6: Array[String] = Array(hello, world)
  f4("hello,world",a=>a.split(","))               //> res7: Array[String] = Array(hello, world)
  f4("hello,world",_.split(","))                  //> res8: Array[String] = Array(hello, world)
  
  val a1=Array(1,2,3,4)                           //> a1  : Array[Int] = Array(1, 2, 3, 4)
  
  a1.foreach {(a:Int)=>{println(a)}}              //> 1
                                                  //| 2
                                                  //| 3
                                                  //| 4
  a1.foreach {a=>println(a)}                      //> 1
                                                  //| 2
                                                  //| 3
                                                  //| 4
  a1.foreach {println(_)}                         //> 1
                                                  //| 2
                                                  //| 3
                                                  //| 4
  a1.filter {(a:Int)=>{a>2}}                      //> res9: Array[Int] = Array(3, 4)
  a1.filter {a=>a>2}                              //> res10: Array[Int] = Array(3, 4)
  a1.filter {_>2}                                 //> res11: Array[Int] = Array(3, 4)
}
```


    defined object Demo03
    



```scala
object Demo04 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  
def f1(n:Int):Int={
  if(n==0) return 2
  if(n==1) return 3
  else f1(n-1)+f1(n-2)
  }                                               //> f1: (n: Int)Int
  
  f1(6)                                           //> res0: Int = 34
  
def f2(n:Int):Int={
  if(n==0) return 2
  if(n==1) return 3
  else f2(n-2)*f2(n-2)
  }                                               //> f2: (n: Int)Int
  
  f2(6)                                           //> res1: Int = 256
  
  def f3(n:Int):Int={
  if(n==0) return 2
  if(n==1) return 3
  if(n%2==0) 2*f3(n-2)
  else 3*f3(n-2)
  
  }                                               //> f3: (n: Int)Int
  
  f3(9)                                           //> res2: Int = 243
}
```


    defined object Demo04
    



```scala
object Demo05 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  val v1=100                                      //> v1  : Int = 100
  lazy val v2=100                                 //> v2: => Int
  println(v2)                                     //> 100
  
  def f1(a:Int,b:Int)={a+b}                       //> f1: (a: Int, b: Int)Int
  def f11(a:Int)(b:Int)={a+b}                     //> f11: (a: Int)(b: Int)Int
  f11(2)(3)                                       //> res0: Int = 5
    
  def f2(a:Int,b:Int,c:Int)={a+b+c}               //> f2: (a: Int, b: Int, c: Int)Int
    
  def f21(a:Int)(b:Int)(c:Int)={a+b+c}            //> f21: (a: Int)(b: Int)(c: Int)Int
  
  def f22(a:Int,b:Int)(c:Int)={a+b+c}             //> f22: (a: Int, b: Int)(c: Int)Int
  
  def f23(a:Int)(b:Int,c:Int)={a+b+c}             //> f23: (a: Int)(b: Int, c: Int)Int
    
  def f3(a:Int,b:Int,f:(Int,Int)=>Int)={f(a,b)}   //> f3: (a: Int, b: Int, f: (Int, Int) => Int)Int
  
  //--重点留意下面这种形式,前面是普通参数,后面是匿名函数
  //--这种形式叫做用户自建的控制结构
  def f31(a:Int,b:Int)(f:(Int,Int)=>Int)={f(a,b)} //> f31: (a: Int, b: Int)(f: (Int, Int) => Int)Int
  
  f31(2,3)(_+_)                                   //> res1: Int = 5
  
  def f32(a:Int)(b:Int,f:(Int,Int)=>Int)={f(a,b)} //> f32: (a: Int)(b: Int, f: (Int, Int) => Int)Int
  
  def f33(a:Int)(b:Int)(f:(Int,Int)=>Int)={f(a,b)}//> f33: (a: Int)(b: Int)(f: (Int, Int) => Int)Int
}
```


    defined object Demo05
    



```scala
import scala.collection.mutable._
object Demo06 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  
  //--声明数组并赋值
  val a1=Array(1,2,3,4)                           //> a1  : Array[Int] = Array(1, 2, 3, 4)
  val a2:Array[Int]=Array(1,2,3,4)                //> a2  : Array[Int] = Array(1, 2, 3, 4)
   
  //--声明一个长度为3的数组
  val a3=new Array[Int](3)                        //> a3  : Array[Int] = Array(0, 0, 0)
  
  //--上面的a1,a2,a3都是定长数组
  //--定长:一经声明,长度不可变
     
  //--声明一个变长数组
  val a4=scala.collection.mutable.ArrayBuffer(1,2,3,4)
                                                  //> a4  : scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2, 3, 4)
  val a5=ArrayBuffer(1,2,3,4)                     //> a5  : scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2, 3, 4)
  
  
  //--通过下标来操作(取值或赋值)数组,scala通过()来操作,不同于java[]
  a1(0)                                           //> res0: Int = 1
  a1.apply(0)                                     //> res1: Int = 1
  
  a1(0)=10
  a1                                              //> res2: Array[Int] = Array(10, 2, 3, 4)
  
  //--append方法是变长数组拥有的方法
  for(i<-5 to 10){
  a4.append(i)
  }
  
  a4                                              //> res3: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2, 3, 4, 5,
                                                  //|  6, 7, 8, 9, 10)
  //--下面学习Array相关的重要的方法
  
  val a6=Array(1,1,2,2,3,8,7,4,5)                 //> a6  : Array[Int] = Array(1, 1, 2, 2, 3, 8, 7, 4, 5)
  
  a6.max                                          //> res4: Int = 8
  a6.min                                          //> res5: Int = 1
  //--去重
  a6.distinct                                     //> res6: Array[Int] = Array(1, 2, 3, 8, 7, 4, 5)
  
  //--根据指定的匿名函数条件计数
  a6.count { x => x%2==0 }                        //> res7: Int = 4
  a6.count { _%2==0 }                             //> res8: Int = 4
  a6.count { _==1}                                //> res9: Int = 2
  
  a6.length                                       //> res10: Int = 9
  
  //--取出前n个元素,并返回到一个新Array中
  val a7=a6.take(2)                               //> a7  : Array[Int] = Array(1, 1)
  //--取出后n个元素,并返回到一个新Array中
  val a8=a6.takeRight(3)                          //> a8  : Array[Int] = Array(7, 4, 5)
  
  //--删除前n个元素,并返回剩余元素到新Array中
  val a9=a6.drop(2)                               //> a9  : Array[Int] = Array(2, 2, 3, 8, 7, 4, 5)
  
  //--删除后n个元素,并返回剩余元素到新Array中
  val a10=a6.dropRight(2)                         //> a10  : Array[Int] = Array(1, 1, 2, 2, 3, 8, 7)
 
  //--返回数组的头元素
  a6.head                                         //> res11: Int = 1
  a6.take(1)                                      //> res12: Array[Int] = Array(1)
  
  //--返回尾元素
  a6.last                                         //> res13: Int = 5
  a6.takeRight(1)                                 //> res14: Array[Int] = Array(5)
  
  //--根据匿名函数过滤,并返回新数组
  val a11=a6.filter { x => x%2==0&&x>4 }          //> a11  : Array[Int] = Array(8)
  
  //--遍历方法,一般用于打印测试
  a6.foreach{println}                             //> 1
                                                  //| 1
                                                  //| 2
                                                  //| 2
                                                  //| 3
                                                  //| 8
                                                  //| 7
                                                  //| 4
                                                  //| 5
 //--将数组元素以指定的分隔符,返回成一个字符串
 a6.mkString("|")                                 //> res15: String = 1|1|2|2|3|8|7|4|5
 
 //--根据匿名函数,判断元素是否存在.
 a6.exists{x=>x>9}                                //> res16: Boolean = false
 
 //--根据匿名函数排序,并返回一个新数组
 val a12=a6.sortBy { x => x }                     //> a12  : Array[Int] = Array(1, 1, 2, 2, 3, 4, 5, 7, 8)
 //--降序排序, - 负号前需要加空格
 val a13=a6.sortBy { x => -x }                    //> a13  : Array[Int] = Array(8, 7, 5, 4, 3, 2, 2, 1, 1)
 
 val a14=Array(1,2,3)                             //> a14  : Array[Int] = Array(1, 2, 3)
 
 val a15=Array(3,4,5)                             //> a15  : Array[Int] = Array(3, 4, 5)
 
 //--取交集,把结果返回到一个新Array
 //--应用:比较多个文件的相同部分
 val a16=a14.intersect(a15).intersect(a6)         //> a16  : Array[Int] = Array(3)
 
 //--取并集,合并数组
 val a17=a14.union(a15).union(a6)                 //> a17  : Array[Int] = Array(1, 2, 3, 3, 4, 5, 1, 1, 2, 2, 3, 8, 7, 4, 5)

 //--取差集,有调用顺序
 //--应用场景:比较文件之间的相异的数据
 a14.diff(a15)                                    //> res17: Array[Int] = Array(1, 2)
 a15.diff(a14)                                    //> res18: Array[Int] = Array(4, 5)
}
```


    defined object Demo06
    



    <console>:61: warning: a pure expression does nothing in statement position; you may be omitting necessary parentheses
      a1                                              //> res2: Array[Int] = Array(10, 2, 3, 4)
      ^
    <console>:68: warning: a pure expression does nothing in statement position; you may be omitting necessary parentheses
      a4                                              //> res3: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2, 3, 4, 5,
      ^
    



```scala
import scala.collection.mutable.ListBuffer

object Demo07 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  
  //--声明定长List
  val l1=List(1,2,3,4)                            //> l1  : List[Int] = List(1, 2, 3, 4)
  
  
  //--声明变长List
  val l2=scala.collection.mutable.ListBuffer      //> l2  : collection.mutable.ListBuffer.type = scala.collection.mutable.ListBuff
                                                  //| er$@22f71333
  
  val l3=ListBuffer                               //> l3  : scala.collection.mutable.ListBuffer.type = scala.collection.mutable.Li
                                                  //| stBuffer$@22f71333
  //--通过下标操作
  l1(0)                                           //> res0: Int = 1
  l1.apply(0)                                     //> res1: Int = 1
  
  //--在List左侧添加元素,并返回一个新List
  val l4=0+:l1                                    //> l4  : List[Int] = List(0, 1, 2, 3, 4)
  
  //--在List右侧添加元素,并返回一个新List
  val l5=l1:+5                                    //> l5  : List[Int] = List(1, 2, 3, 4, 5)
  
  //--其他的方法,Array有的,List也有
    l1.filter { x => x>2 }                          //> res2: List[Int] = List(3, 4)
  l1.foreach{println}
    //--集合间的类型转换,形式:to类型
  //--类型转换:比如某种集合类型没有distinct,可以通过类型转换来实现
  val a1=l1.toArray                               //> a1  : Array[Int] = Array(1, 2, 3, 4)
  
  val l6=List(1,1,2,2,3)                          //> l6  : List[Int] = List(1, 1, 2, 2, 3)
  
  l6.toArray.distinct.toList                      //> res3: List[Int] = List(1, 2, 3)
  
  //--反转
  l6.reverse                                      //> res4: List[Int] = List(3, 2, 2, 1, 1)
  
  val l7=List(2,1,5,4,3)                          //> l7  : List[Int] = List(2, 1, 5, 4, 3)
  
  val l8=l7.sortBy { x => x }.reverse             //> l8  : List[Int] = List(5, 4, 3, 2, 1)
}
```


    defined object Demo07
    



```scala
object Demo08 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  
  //--声明一个定长set,不包含重复元素
  val s1=Set(1,1,2,2,3)                           //> s1  : scala.collection.immutable.Set[Int] = Set(1, 2, 3)
  
  //--声明一个边长Set
  val s2=scala.collection.mutable.Set(1,2,3,4)    //> s2  : scala.collection.mutable.Set[Int] = Set(1, 2, 3, 4)
  
  val s3=Set(1,2,3)                               //> s3  : scala.collection.immutable.Set[Int] = Set(1, 2, 3)
  val s4=Set(3,4,5)                               //> s4  : scala.collection.immutable.Set[Int] = Set(3, 4, 5)
  //--取交集
  s3.intersect(s4)                                //> res0: scala.collection.immutable.Set[Int] = Set(3)
  s3&s4                                           //> res1: scala.collection.immutable.Set[Int] = Set(3)
  
  //--取差集
  s3.diff(s4)                                     //> res2: scala.collection.immutable.Set[Int] = Set(1, 2)
  s3&~s4                                          //> res3: scala.collection.immutable.Set[Int] = Set(1, 2)
  
  //--合并set
  s3.union(s4)                                    //> res4: scala.collection.immutable.Set[Int] = Set(5, 1, 2, 3, 4)
  s3++s4                                          //> res5: scala.collection.immutable.Set[Int] = Set(5, 1, 2, 3, 4)
    
  val s5=Set(1,2,3,4,5,6,7)                       //> s5  : scala.collection.immutable.Set[Int] = Set(5, 1, 6, 2, 7, 3, 4)
  
  //--将一个Set拆成两个子Set,4表示一个子Set的元素个数是4个,另外一个3个
  //--应用场景:将一个数据集拆成两个子集,一个用于样本集,另一个用于测试集
  s5.splitAt(4)                                   //> res6: (scala.collection.immutable.Set[Int], scala.collection.immutable.Set[I
                                                  //| nt]) = (Set(5, 1, 6, 2),Set(7, 3, 4))
}
```


    defined object Demo08
    



```scala
object Demo09 {
  //--声明一个定长Map
  val m1=Map("tom"->23,"rose"->35,"jim"->30)      //> m1  : scala.collection.immutable.Map[String,Int] = Map(tom -> 23, rose -> 35 
                                                  //| , jim -> 30)
  
  //--声明变长Map,可以追加新的KV对
  val m2=scala.collection.mutable.Map("tom"->23,"rose"->35,"jim"->30)
                                                  //> m2  : scala.collection.mutable.Map[String,Int] = Map(jim -> 30, rose -> 35, 
                                                  //| tom -> 23)
  //--通过key取值
  m1("tom")                                       //> res0: Int = 23
  m1.apply("tom")                                 //> res1: Int = 23
  //--获取map的key的迭代器
  m1.keys.foreach{println}                        //> tom
                                                  //| rose
                                                  //| jim
  //--获取map的value的迭代器
  m1.values.toList.distinct                       //> res2: List[Int] = List(23, 35, 30)
  //--针对变长Map追加新的KV对
  m2+=("jary"->40)                                //> res3: Demo09.m2.type = Map(jary -> 40, jim -> 30, rose -> 35, tom -> 23)
  //--映射方法,专用于操作Map类型的value
  m1.mapValues { x => x*2 }                       //> res4: scala.collection.immutable.Map[String,Int] = Map(tom -> 46, rose -> 70
                                                  //| , jim -> 60)
  m1.map{case(k,v)=>(k,v*2)}                      //> res5: scala.collection.immutable.Map[String,Int] = Map(tom -> 46, rose -> 70
                                                  //| , jim -> 60)
  //--get通过key取值,并可以指定没有对应key值的默认值
  m1.get("zs").getOrElse(0)                       //> res6: Int = 0
  m1.contains("tom")                              //> res7: Boolean = true
  
  m1.size                                         //> res8: Int = 3
}
```


    defined object Demo09
    



```scala
object Demo10 {
  println("Welcome to the Scala worksheet")       //> Welcome to the Scala worksheet
  
  //--声明一个tuple,含5个元素
  val t1=(1,2,3,4,5)                              //> t1  : (Int, Int, Int, Int, Int) = (1,2,3,4,5)
  
  
  val t2=(1,"hello",Array(1,2,3),Map("tom"->23))  //> t2  : (Int, String, Array[Int], scala.collection.immutable.Map[String,Int]) 
                                                  //| = (1,hello,Array(1, 2, 3),Map(tom -> 23))
  //--tuple的取值
  t1._3                                           //> res0: Int = 3
  t2._2                                           //> res1: String = hello
  
  val t3=(1,2,(1,2,3,4))                          //> t3  : (Int, Int, (Int, Int, Int, Int)) = (1,2,(1,2,3,4))
  
  t3._3._4                                        //> res2: Int = 4
  
  //--针对Array操作Tuple时,类型需要一致
  val t4=("hello",100,Array((1,2,3),(2,3,4),(3,4,5),(6,7,8)))
                                                  //> t4  : (String, Int, Array[(Int, Int, Int)]) = (hello,100,Array((1,2,3), (2,3
                                                  //| ,4), (3,4,5), (6,7,8)))
   
  t4._3(3)._3                                     //> res3: Int = 8
  
  //--下面表示声明一个Array,泛型是二元Tuple
  val a1=Array((1,2),(2,3),(3,4))                 //> a1  : Array[(Int, Int)] = Array((1,2), (2,3), (3,4))
}
```


    defined object Demo10
    



    <console>:49: warning: a pure expression does nothing in statement position; you may be omitting necessary parentheses
      t1._3                                           //> res0: Int = 3
         ^
    <console>:50: warning: a pure expression does nothing in statement position; you may be omitting necessary parentheses
      t2._2                                           //> res1: String = hello
         ^
    <console>:54: warning: a pure expression does nothing in statement position; you may be omitting necessary parentheses
      t3._3._4                                        //> res2: Int = 4
            ^
    



```scala
object Demo11 {
    val l1=List("hello","world","hello","1811")     //> l1  : List[String] = List(hello, world, hello, 1811)
    //--List[String]->List[(String,Int)]

    //--map映射方法,把元素从一个形式映射到另外一个形式,并返回一个新集合
    //--map方法只改变元素的形式,不改变元素的个数
    val l2=l1.map { x => (x,1) }                    //> l2  : List[(String, Int)] = List((hello,1), (world,1), (hello,1), (1811,1))

    //--操作l2 List[(String,Int)]->List[String]
    val l3=l2.map{x=>x._1}                          //> l3  : List[String] = List(hello, world, hello, 1811)

    val l4=List(("tom",18),("rose",25),("jim",20),("jary",15))
                                                  //> l4  : List[(String, Int)] = List((tom,18), (rose,25), (jim,20), (jary,15))
    //--操作l4,过滤出年龄大于18岁的数据

    val l5=l4.filter{x=>x._2>18}                    //> l5  : List[(String, Int)] = List((rose,25), (jim,20))

    //--操作l4,按年龄做升序排序
    val l6=l4.sortBy{x=> -x._2}                     //> l6  : List[(String, Int)] = List((rose,25), (jim,20), (tom,18), (jary,15))

    val m1=Map("tom"->23,"rose"->18,"jim"->30)      //> m1  : scala.collection.immutable.Map[String,Int] = Map(tom -> 23, rose -> 18
                                                  //| , jim -> 30)

    //--操作m1,过滤出年龄大于20岁的数据
    //--针对Map类型,底层会将kv对封装为二元Tuple(key,value)
    val m2=m1.filter{x=>x._2>20}                    //> m2  : scala.collection.immutable.Map[String,Int] = Map(tom -> 23, jim -> 30)
                                                  //| 
    val m3=m1.filter{case(k,v)=>v>20}               //> m3  : scala.collection.immutable.Map[String,Int] = Map(tom -> 23, jim -> 30)
    
    //--用reduce方法 计算 1~6的阶乘结果
    //--①a=1 b=2 a*b=2
    //--②a=2 b=3 a*b=6
    //--③a=6 b=4 a*b=24
    1 to 6 reduce{(a,b)=>a*b}                 //> res0: Int = 720

    val l7=List("hello,world","hello,hadoop","hello,1811")
                                                      //> l7  : List[String] = List(hello,world, hello,hadoop, hello,1811)
    //--List[String]->List[Array[String]]
    val l8=l7.map { x => x.split(",") }       //> l8  : List[Array[String]] = List(Array(hello, world), Array(hello, hadoop),
                                                      //|  Array(hello, 1811))

    //--扁平化map方法,也是映射方法,会概念元素的形式,此外元素个数也会变化
    val l9=l7.flatMap { x => x.split(",") }   //> l9  : List[String] = List(hello, world, hello, hadoop, hello, 1811)

    //--按指定的匿名函数分组,并返回一个Map
    //--Map的key是分组的条件,Map的Value是相同key聚合后的List
    val m4=l9.groupBy { x => x }              //> m4  : scala.collection.immutable.Map[String,List[String]] = Map(hadoop -> L
                                                      //| ist(hadoop), world -> List(world), 1811 -> List(1811), hello -> List(hello,
                                                      //|  hello, hello))
      val l10=List(("bj",1),("sh",2),("bj",3),("sh",4))
                                                      //> l10  : List[(String, Int)] = List((bj,1), (sh,2), (bj,3), (sh,4))

     //--操作l10,按地区分组

     val m5=l10.groupBy{x=>x._1}               //> m5  : scala.collection.immutable.Map[String,List[(String, Int)]] = Map(bj -
                                                      //| > List((bj,1), (bj,3)), sh -> List((sh,2), (sh,4)))
}
```


    defined object Demo11
    



```scala
object Demo12 {
  val l1=List("hello,world","hello,world","hello,1811")         //> l1  : List[String] = List(hello,world, hello,world, hello,1811)
  l1.flatMap { line => line.split(",") }
  .groupBy { word => word }
  .mapValues { list => list.size }
  .toList                                   //> res0: List[(String, Int)] = List((world,2), (1811,1), (hello,3))
  l1.flatMap { line => line.split(",") }
  .groupBy { word => word }
  .map {case(k,v)=>(k,v.size)}
  .toList                                   //> res1: List[(String, Int)] = List((world,2), (1811,1), (hello,3))
   l1.flatMap { line => line.split(",") }
  .map { word =>(word,1) }
  .groupBy{case(word,one)=>word}
    .mapValues{list=>list.map{x=>x._2}.reduce{_+_}}
    .toList                                       //> res2: List[(String, Int)] = List((world,2), (1811,1), (hello,3))
  l1.flatMap { line => line.split(",") }
  .map { word =>(word,1) }
  .groupBy{case(word,one)=>word}
    .mapValues{list=>list.map{x=>x._2}.sum}
    .toList                                       //> res3: List[(String, Int)] = List((world,2), (1811,1), (hello,3))
  val l2=l1.flatMap { _.split(",") }
  .map { (_,1) }
  .groupBy{_._1}
    .mapValues{_.map{_._2}.sum}
    .toList                                       //> l2  : List[(String, Int)] = List((world,2), (1811,1), (hello,3))
    
  //--操作l2,取出频次最高的那一项单词数据   (hello,3)
  
  l2.sortBy{x=> -x._2}.take(1)                    //> res4: List[(String, Int)] = List((hello,3))
}
```


    defined object Demo12
    



```scala

```


```scala

```


```scala

```


```scala

```
