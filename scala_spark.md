
- 创建SparkSession  
import org.apache.spark.sql.SparkSession  
val spark = SparkSession.builder().master("local").appName("asdsad").getOrCreate()  
可用sc.stop()停止，与变量名无关（如spark）
- 读取hadoop数据  
val hd_dt = spark.read.format("csv").option("header", "false").load("hdfs://172.16.1.122:9000/whl/data.csv")
- 读取本地csv数据  
val lc0 = spark.read.format("csv")    
.option("inferSchema","true")  
.option("delimiter",",")  
.option("header", "false")  
.option("mode", "DROPMALFORMED")  // 丢弃异常值  
.option("nullValue","???")   // null值填充  
.load("file:///home/whl/taxi_location.csv")  
- 使用schema读取数据  
import org.apache.spark.sql.types._  
val custom = StructType(Array(  
    StructField("id1", StringType, true),  
    StructField("id8", StringType, true)  
))  
val lc3 = spark.read.format("csv")  
.schema(custom)  
.load("file:///home/whl/taxi_location.csv")   
- 使用sc.textFile读取（如何设置第1行为列名？）  
val rec = sc.textFile("file:///home/whl/iris_df.csv").map(line=>line.split(","))  
- 创建临时视图，并用sql操作（lc0.registerTempTable("users")在2.0版本已被createOrReplaceTempView替换）  
lc0.createOrReplaceTempView("temp_name")  // 此视图的生命周期依赖于SparkSession类，如果想drop此视图可采用dropTempView删除，spark.catalog.dropTempView(“tempViewName”)  
val temple = spark.sql("select * from temp_name limit 5")  
val max = spark.sql("select max(col) from temp_name")  
lc0.createGlobalTempView("temp_name")  // 这种视图的生命周期取决于spark application本身。如果想drop此视图可采用dropGlobalTempView删除，spark.catalog.dropGlobalTempView(“tempViewName”)  
- 导出到single csv，但是创建一个文件夹，且文件名乱码  
lc0.write.option("header","true").csv("file:///home/whl/asdfd.csv")

- obj.getClass.getSimpleName  查看对像类型  
- obj.getClass.getTypeName  同上  
- var.hashCode  变量内存地址  
- spark.udf.register("asdf", (a:Int,b:Int)=>{a+b})  自定义函数  
- sc.stop()  不仅可以停止SparkContext，还可以停止spark=SparkSession  

- 打印数据格式  
lc0.printSchema  
- 显示列名  
lc0.columns
- 统计行数  
lc0.count
- 显示前n行数据  
lc0.show(n,truncate=false)  

- 运算符

# groupBy  
lc0.groupBy("_c1").count().count()  
lc0.groupBy("_c1").count().sort("count")

# trick
- 通过：_星，将前面的list,array,range等数据打散  
val ary4 = Array(1 to 10 : _*)

# map与mapPartitions
- 常规  
df.rdd.map(row => (Integer.parseInt(row(0).toString),row(1).toString))  
raw_df.map(line => line.split("\t")) 
- 分区创建  
var aa = sc.parallelize(1 to 7, 2)    
aa.collect    
- map方法  
val aa_m1 = aa.map(x => x+1)  
aa_m1.collect  
- mapPartitions方法，还没完全理解  
val aa_m2 = aa.mapPartitions(x => {var result = List[Int]();var cur = 0;while(x.hasNext){cur += x.next()};result.::(cur).iterator})  
aa_m2.collect  

- 选取一列数据  
val c10_array = lc0.select("_c10").collect()  



# 类型转换
List(1,2,3,4).toArray
- map转化为ArrayBuffer  
val res1 = mx.toSeq.sortBy(_._1)  
- string转化  
val res2 = "123".toInt   
val res3 = "123".toDouble   
- 将string转为int  
import org.apache.spark.sql.types._  
val res4 = Integer.parseInt(c10_array(1)(0).toString)

# 字符串类型  
- 创建  
val s1:String="hello,world"  
- 切分，截取，截除，重复，去重，反转  
val s2=s1.split(" ")   // s1:Array[String] = Array(hello, world)  
val s3=s1.take(5);val s4=s1.takeRight(5)    
val s5=s1.drop(5);   val s6=s1.dropRight(5)    
val s7=s1*3  
val s8=s1.distinct  
val s9=s1.reverse  

# Array类型  
- 创建，索引  
val res0=new Array[Int]（3）  // 创建长度为3的数组  
val res0:Array[Int]=Array(1,2,3,4)     
val res0:Array[String]=Array("a","b")    
val res4=scala.collection.mutable.ArrayBuffer(1,2,3,4)  
val value0 = Array(1,2,3,4,5,6)  
val Array(v1,v2,_*) = value0                           
- 下标来操作(取值或赋值)数组,scala通过()来操作,不同于java[]
val a1=Array(1,2,3,4)    
a1(0)   
a1.apply(0)  
a1(0)=10  
- 可变Array操作
var numArrayBuffer = new scala.collection.mutable.ArrayBuffer[Int]()  
numArrayBuffer += 1  
numArrayBuffer += (2, 3, 4, 5)  
numArrayBuffer ++= Array(6, 7, 8, 9, 10)  
numArrayBuffer.insert(5, 12)   // 在第5个位置插入12  
numArrayBuffer.insert(3, 22, 23, 24, 25)  // 在第3个位置插入之后所有数字  
numArrayBuffer.remove(1)  
numArrayBuffer.remove(1, 5)  // 移除1到5元素  
numArrayBuffer.toArray  // 相互转化  
numArrayBuffer.toBuffer  // 相互转化  
numArrayBuffer.trimEnd(5)  // 从尾部截取  
for(i<-5 to 10){numArrayBuffer.append(i)}  // append
- Array相关方法  
val a6=Array(1,1,2,2,3,8,7,4,5)   
a6.max;a6.min;a6.distinct;a6.length                            
val a7=a6.take(2)           // 返回新数组      
val a8=a6.takeRight(3)      // 返回新数组  
val a9=a6.drop(2)           // 返回新数组  
val a10=a6.dropRight(2)     // 返回新数组  
a6.head;a6.last                           
a6.count { x => x除2双等于0 }    // 按条件统计  
a6.count { _除2双等于0 }         // 按条件统计      
a6.count { _双等于1}            // 按条件统计  
val a11=a6.filter { x => x除2双等于0&&x>4 }  // 根据匿名函数过滤,并返回新数组  
a6.foreach{println}   // 遍历，一般用于打印  
a6.mkString("|")   // 将数组元素以指定的分隔符,返回成一个字符串      
a6.exists{x=>x>9}   // 根据匿名函数,判断元素是否存在.                         
val a12=a6.sortBy { x => x }   // 根据匿名函数排序,并返回一个新数组              
val a13=a6.sortBy { x => -x }   // 降序排序,负号前需要加空格   
val a14=Array(1,2,3)                         
val a15=Array(3,4,5)                         
val a16=a14.intersect(a15).intersect(a6)  // 取交集   
val a17=a14.union(a15).union(a6)   // 取并集，合并数组          
a14.diff(a15)   // 取差集                             
a15.diff(a14)   // 取差集     
- 其他  
res11.take(5).foreach({line => line.foreach(print);println})
- 这？  
val res1=Array(1,Array(22,33,44),3,4)  
res1(1)(0)

# List类型
- 常规方法  
val l1=List(3,2,1,4,3)   
val l2=scala.collection.mutable.ListBuffer(2,4,6)  
l1(0)  
l1.apply(0)   
l1.reverse  
l1.sortBy { x => x }.reverse  
l1.toArray.distinct.toList  
val l4=0+:l1   // 左添加元素  
val l5=l1:+5   // 右添加元素  
- 其他的方法,Array有的,List也有  
val newNames = List.range(0, 17).mkString(",").split(",")   
l1.filter { x => x>2 }  
l1.foreach{println}  
val LL = new scala.collection.mutable.LinkedList()  // 创建链表型list
- 3冒号合并为新List  
val a = List(1, 2,3)  
val b = List(2,3, 4)  
val c = a ::: b  
- 2冒号合并List与元素，左侧必须是list  
val a = Array(1, 2,3)  
val b = List(1 ,"a")  
val c = a :: b  
- +: 和 :+方法，分别从左侧右侧加入  
val a = List(1, 2,3)   
val b = List(2,3, 4)  
a:+b  
7+:a  

# Set类型  
- 常规方法
val s1=Set(1,1,2,2,3)                         
val s2=scala.collection.mutable.Set(1,2,3,4)  
val s3=Set(1,2,3)   
val s4=Set(3,4,5)   
s3.intersect(s4)    // 取交集  
s3&s4               // 取交集  
s3.diff(s4)         // 取差集  
s3&~s4              // 取差集  
s3.union(s4)        // 取并集  
s3++s4              // 取并集

# tuple类型
- 常规  
val t2=(1,"hello",Array(1,2,3),Map("tom"->23))  
t2._2(2)  
t2._4.keys  
val t4=("hello",100,Array((1,2,3),(2,3,4),(3,4,5),(6,7,8)))  
t4._3(3)._3  
val a1=Array((1,2),(2,3),(3,4))   
- 箭头组成元组  
val a = 1  
val b = 2  
a -> b  

# map类型  
- 创建  
val m1 = scala.collection.mutable.Map(0 -> 0)  // 可用m1+=()扩充，可用m1()=new扩充  
val m2 = scala.collection.immutable.Map(0 -> 0)  // 完全不可扩充，且不可m2(old_key)=new_value进行更新  
var m3 = scala.collection.mutable.Map(0 -> 0)  // 可用m1+=()扩充，可用m1()=new扩充  
var m4 = scala.collection.immutable.Map(0 -> 0)    // 可用m1+=()扩充，不可m1()=new扩充，且不可m2(old_key)=new_value进行更新  
- 取值  
m1.apply(key)  
m1(key)  
- 获取key和value做一些操作  
val m1=Map("tom"->23,"rose"->35,"jim"->30)   
m1.keys.foreach{println}  
m1.values.toList.distinct  
- 其他  
m2+=("jary"->40)     // 针对变长增加新的k,v对  
m1.mapValues{x => x*2}  // 专用于value操作  
m1.map{case(k,v)=>(k,v*2)}  
m1.get("zs").getOrElse(0)    // 过key取值,并设置缺省值  
m1.contains("tom")           
m1.size                      

# if语句
val r1=if(x>5)println("big") else println("small")

# while语句
while(index<5){println(index);index+=1}  

# for循环
for(i<-Array(1,3,5))println(i)  
for(i<-1.to(7);j<-3 to 8;if i>2;if j>6&&i%2双等于0) println(i,j)  
for(a<-1 to 9){for(b<-1 to a){print(b+"*"+a+"="+b*a+"\t")};println()}  
for(a<-1 to 9;b<-1 to a;val sep=if(b==a)"\r\n" else "\t")print(b+"*"+a+"="+b*a+sep)  
for(a<-1 to 9;b<-1 to a;val sep=if(b==a)"\r\n" else "\t"){print(s"$b*$a=${b*a}$sep")}  
for(i<-Map("tom"->23,"rose"->30,"tom"->35)){println(i)}  
for((k,v)<-Map("tom"->23,"rose"->30,"tom"->35)){println(k);println(v)}  
val res1 = for(i<-List(2,4,6))yield{i乘2}  
val res2 = for(i<-Array(2,4,6))yield{i乘2}  
val m2=for((k,v)<-Map("book"->10,"gun"->100,"ipad"->1000))yield{(k,v*0.9)}         
for(i<-1 to 10 reverse)println(i) 
for(i<-10 to 1 by -1)println(i) 

# 迭代器，可用while和for来遍历
val iter = Iterator("Hadoop","Spark","Scala")  
while (iter.hasNext) {println(iter.next())}  
val iter2 = Iterator("python","Spark","Scala")
for (elem <- iter2) { println(elem)}

# 聚类建模toy
- 读取数据  
val iris = spark.read.format("csv")  
.option("inferSchema","true")  
.option("delimiter",",")  
.option("header", "true")  
.option("mode", "DROPMALFORMED")  
.option("nullValue","???")  
.load("file:///home/whl/iris_df.csv")  
- 特征combine  
import org.apache.spark.ml.feature.VectorAssembler  
val assembler = new VectorAssembler().setInputCols(iris.columns.take(4)).setOutputCol("features")  
val combine_feature = assembler.transform(iris).select("features","category")  
- 模型训练  
import org.apache.spark.ml.clustering.KMeans  
val fst_kmeans = new KMeans().setK(3).setSeed(100L).setMaxIter(500)  
val mod = fst_kmeans.fit(features_vec)  
val res = mod.transform(features_vec)  
mod.explainParams()  // 超参解读  
mod.extractParamMap  // 显示参数值  



# FPGrouwth建模toy
- import org.apache.spark.mllib.fpm.FPGrowth  
- 读数据的方式  
val res1 = sc.textFile("file:///home/whl/apriori_data.txt").map(line=>line.split(", "))
val fpg = new FPGrowth()  
val fpg_m1 = fpGroup.setMinSupport(0.1).setNumPartitions(1).run(res1)  //设置支持度，设置partitions  
val fpg_m1_frq = fpg_m1.freqItemsets.collect  // 获取频繁项集
val fpg_cfd = fpg_m1.generateAssociationRules(0.7).collect()  // 获取关联规则及其提升度，只记算满足上步支持度的项  
val x = fpg_m1.itemSupport("item")  // 暂时用法不知道，只返回单项的支持度  
- 造数据的方式   
val test_1 = Seq("a","a b","a b c","a b c d","a b c d e").map(_.split(" ")).toArray  // 不用toArray也是可以的
val test_rdd1 = sc.parallelize(test_1, 1)  // 一定要rdd之后才可以导入模型，可能是因为mllib库的fpm吧
val fpg1 = new FPGrowth()  
val fpg1_m1 = fpGroup.setMinSupport(0.8).setNumPartitions(1).run(test_rdd1)  
val fpg1_m1_frq = fpg1_m1.freqItemsets.collect  
val fpg_cfd = fpg1_m1.generateAssociationRules(0.7).collect()  

# DataFrame，在scala中，DataFrame只是Dataset [Row]的类型别名
- 读文件直接创建DataFrame  
val df1 = spark.read.format("csv").option("header", "true").load(path)
- 创建dataframe并指定列名  
val df2 = spark.createDataFrame(Seq(  
  (0, "Hi I heard about Spark", 3.0),  
  (1, "I wish Java could use case classes", 4.0),  
  (2, "Logistic regression models are neat", 4.0)  
)).toDF("id", "text", "rating")  
- 重命名列名    
val df3 = df2.toDF(Array("a","b","c"):_*)  
- 添加新列  
val df4 = df3.withColumn("newcolumn", df3("c") * 2)  
- 打印列的元素类型  
df4.printSchema  
- 修改列的元素类型  
val df5 = df4.withColumn("newcolumn", df4("newcolumn").cast("int"))  

# 矩阵
- 基本操作  
import breeze.linalg._  
import breeze.numerics._  
val m1 = DenseMatrix.zeros[Double](2,3)   // 2行3列的0矩阵  
val v1 = DenseVector.zeros[Double](3)     // 长度为3的0向量  
val v2 = DenseVector.ones[Double](3)      // 长度为3的1向量  
val v3 = DenseMatrix.fill(2,3)(5.0)         // 创建指定元素的向量，长度为3，元素为5  
val v4 = DenseVector.range(1,10,2)        // 根据范围创建向量参数（start，end，step），output： 1 3 5 7 9  
val m2 = DenseMatrix.eye[Double](3)       // 创建对角线为1的矩阵，3行3列的单元矩阵  
val m7 = diag(DenseVector(1.0,2.0,3.0))   // 创建指定对角线元素的矩阵，3行3列，对角元素分别为1 2 3  
val m3 = DenseMatrix((1.0,2.0),(3.0,4.0)) // 根据向量创建矩阵，每个数组就是一行  
val v8 = DenseVector(1,2,3,4)             // 根据元素创建向量  
- 转置  
m3.t  
- 根据下标创建向量和矩阵  
val v10 = DenseVector.tabulate(5){i=>2*i}  
val m4 = DenseMatrix.tabulate(3,2){case(i,j) => i+j}  
- 根据数组创建向量和矩阵（结果同v8）（2行3列，元素分别为Array的元素）  
val v11 = new DenseVector(Array(1,2,3,4))                
val m5 = new DenseMatrix(2,3,Array(11,12,12,21,21,11))    
- 创建随机向量和矩阵  
val v12 = DenseVector.rand(4)  
val m6 = DenseMatrix.rand(2,3)  
- 向量元素访问  
val a = DenseVector(1,2,3,4,5,6,7,8,9)   
val ao1 = a(0)              
val ao2 = a(1 to 4)         
val ao3 = a(5 to 1 by -1)   
val ao4 = a(1 to -1)        
val ao5 = a(-1)             
- 矩阵元素访问  
val m = DenseMatrix((1.0,2.0,3.0),(4.0,5.0,6.0),(7.0,8.0,9.0))  
val mo1 = m(0,1)  // 访问0行1列的元素  
val mo2 = m(::,1)  // 访问第1列元素  
val mo21 = m.cols  // 取矩阵列数  
val mo3 = m(1,::)  // 访问第1行  
val mo31 = m.rows  // 取矩阵行数  
m(1 to 2, 1 to 2)  
- 元素操作  
val m_1 = DenseMatrix((1.0,2.0,3.0),(4.0,5.0,6.0))  
val m_1o1 = m_1.reshape(3,2)  // 变成3行2列的矩阵  
val m_1o2 = m_1.toDenseVector // 转换成向量, output: DenseVector(1.0, 4.0, 2.0, 5.0, 3.0, 6.0)  
val m_3 = DenseMatrix((1,2,3),(4,5,6),(7,8,9))  
val m_3o1 = lowerTriangular(m_3) // 取下三角，output：((1 0 0) (4  5  0) (7  8  9))  
val m_3o2 = upperTriangular(m_3) // 取上三角，output: ((1 2 3) (0 5 6) (0 0 9))  
val m_3o3 = m_3.copy            // copy生成一个新的矩阵  
val m_3o4 = diag(m_3)           // 对角线生成一个向量，output: DenseVector(1, 5, 9)  
m_3(::,2) := 5                  // 将第2列的元素全部改成5  
m_3(1 to 2,1 to 2) := 666       // 将第2,3列2,3行的元素全部改成666  
- 矩阵的连接（向量的连接和矩阵类似）  
val a1 = DenseMatrix((1,2,3),(4,5,6))  
val a2 = DenseMatrix((1,1,1),(2,2,2))   
val a12V = DenseMatrix.vertcat(a1,a2) // 竖直的连接, output: ((1 2 3) (4 5 6) (1 1 1) (2 2 2))  
val a12H = DenseMatrix.horzcat(a1,a2) // 水平连接，output: ((1 2 3 1 1 1) (4 5 6 2 2 2))  
- 数值计算  
val a_3 = DenseMatrix((1,2,3),(4,5,6))  
val b_3 = DenseMatrix((1,1,1),(2,2,2))  
val ab31 = a_3 + b_3       // 对应元素相加  
val ab32 = a_3 :* b_3      // 对应元素相乘  
val ab33 = a_3 :/ b_3      // 对应元素取商，注意输出为整数商  
val ab34 = a_3 :< b_3      // 对应元素进行判断  
val ab35 = a_3 :== b_3     // 对应元素是否相等  
a_3 :+= 1                   // 所有元素+1，注意此时a_3已经改变  
a_3 :*= 2                   // 所有元素*2  
val aMax = max(a_3)         // 求最大值，output: 14  
val aMaxIndex = argmax(a_3) // 最大值位置的索引, output: (1, 2)  
val ab38 = DenseVector(1,2,3,4) dot DenseVector(1,1,1,1) // 内积，output: 10  
- 求和函数  
val a_4 = DenseMatrix((1,2,3),(4,5,6),(7,8,9))  
val a41 = sum(a_4)         // 所有元素求和，output: 45  
val a42 = sum(a_4,Axis._0) // 每一列进行求和, output: DenseVector(12, 15, 18)  
val a43 = sum(a_4,Axis._1) // 每一行进行求和, output: DenseVector(6, 15, 24)  
val a44 = trace(a_4)       // 对角线求和, output: 15  
val a45 = accumulate(DenseVector(1,2,3,4)) // 分别求前1,2,3,4个元素的和，output: DenseVector(1, 3, 6, 10)  
- 布尔运算  
val a_5 = DenseVector(true,false,true)  
val b_5 = DenseVector(false,true,true)  
val ab51 = a_5 :& b_5 // 对应元素“与”  
val ab52 = a_5 :| b_5 // 对应元素“或”  
val ab53 = !a_5       // 取“非”  
val a_5_2 = DenseVector(7, 8, 9)  
val ab54 = any(a_5_2)//任意一个元素 > 0 即为true  
val ab55 = all(a_5_2)//所有元素 > 0 则为true  

- ？？？下面的索引不正确
val res1=Array(1,Array(22,33,44),3,4)  
res1(1)(0)
- ？？？  
array,list等，如何截取中间几个数？
- ？？？  这是什么类型数据  
val xx = Seq(1,2,3)
- ？？？ 
- ？？？ 
- ？？？ 
- ？？？ 
- ？？？ 


- 1
val res1 = sc.parallelize(List(1,2,3))

- 1  
val input = sc.parallelize(List("Hello world ! Welcome to Spark world . Let's study Spark together !"))  如何查看有几个partion?  
val words = input.flatMap(line => line.split(" "))  
val counts = words.map(word => (word, 1)).reduceByKey((a, b) => a + b)  
counts.foreach(println)  


- 1
如何查看map定义的内部元素类型

# cache策略（cache()是persist()的特例，persist可以指定一个StorageLevel。StorageLevel的列表可以在StorageLevel伴生单例对象中找到）

- cache源码  
/** Persist this RDD with the default storage level (`MEMORY_ONLY`). */  
 def cache(): this.type = persist()  
- persist源码  
 /** Persist this RDD with the default storage level (`MEMORY_ONLY`). */  
  def persist(): this.type = persist(StorageLevel.MEMORY_ONLY)  
- MEMORY_ONLY使用未序列化的Java对象格式，将数据保存在内存中。如果内存不够存放所有的数据，则数据可能就不会进行持久化。那么下次对这个RDD执行算子 操作时，那些没有被持久化的数据，需要从源头处重新计算一遍。这是默认的持久化策略，使用cache()方法时，实际就是使用的这种持久化策略。
- MEMORY_AND_DISK使用未序列化的Java对象格式，优先尝试将数据保存在内存中。如果内存不够存放所有的数据，会将数据写入磁盘文件中，下次对这个RDD执行算子时，持久化在磁盘文件中的数据会被读取出来使用。
- MEMORY_ONLY_SER基本含义同MEMORY_ONLY。唯一的区别是，会将RDD中的数据进行序列化，RDD的每个partition会被序列化成一个字节数组。这种方式更加节省内存，从而可以避免持久化的数据占用过多内存导致频繁GC。
- MEMORY_AND_DISK_SER基本含义同MEMORY_AND_DISK。唯一的区别是，会将RDD中的数据进行序列化，RDD的每个partition会被序列化成一个字节数组。这种方式更加节省内存，从而可以避免持久化的数据占用过多内存导致频繁GC。
- DISK_ONLY使用未序列化的Java对象格式，将数据全部写入磁盘文件中。
- MEMORY_ONLY_2, MEMORY_AND_DISK_2, 等等.对于上述任意一种持久化策略，如果加上后缀_2，代表的是将每个持久化的数据，都复制一份副本，并将副本保存到其他节点上。这种基于副本的持久化 机制主要用于进行容错。假如某个节点挂掉，节点的内存或磁盘中的持久化数据丢失了，那么后续对RDD计算时还可以使用该数据在其他节点上的副本。如果没有 副本的话，就只能将这些数据从源头处重新计算一遍了。

# 如何选择一种最合适的持久化策略
- 默认情况下，性能最高的当然是MEMORY_ONLY，但前提是你的内存必须足够足够大，可以绰绰有余地存放下整个RDD的所有数据。因为 不进行序列化与反序列化操作，就避免了这部分的性能开销；对这个RDD的后续算子操作，都是基于纯内存中的数据的操作，不需要从磁盘文件中读取数据，性能 也很高；而且不需要复制一份数据副本，并远程传送到其他节点上。但是这里必须要注意的是，在实际的生产环境中，恐怕能够直接用这种策略的场景还是有限的， 如果RDD中数据比较多时（比如几十亿），直接用这种持久化级别，会导致JVM的OOM内存溢出异常。
- 如果使用MEMORY_ONLY级别时发生了内存溢出，那么建议尝试使用MEMORY_ONLY_SER级别。该级别会将RDD数据序列化 后再保存在内存中，此时每个partition仅仅是一个字节数组而已，大大减少了对象数量，并降低了内存占用。这种级别比MEMORY_ONLY多出来 的性能开销，主要就是序列化与反序列化的开销。但是后续算子可以基于纯内存进行操作，因此性能总体还是比较高的。此外，可能发生的问题同上，如果RDD中 的数据量过多的话，还是可能会导致OOM内存溢出的异常。
- 如果纯内存的级别都无法使用，那么建议使用MEMORY_AND_DISK_SER策略，而不是MEMORY_AND_DISK策略。因为 既然到了这一步，就说明RDD的数据量很大，内存无法完全放下。序列化后的数据比较少，可以节省内存和磁盘的空间开销。同时该策略会优先尽量尝试将数据缓 存在内存中，内存缓存不下才会写入磁盘。
- 通常不建议使用DISK_ONLY和后缀为_2的级别：因为完全基于磁盘文件进行数据的读写，会导致性能急剧降低，有时还不如重新计算一次 所有RDD。后缀为_2的级别，必须将所有数据都复制一份副本，并发送到其他节点上，数据复制以及网络传输会导致较大的性能开销，除非是要求作业的高可用 性，否则不建议使用。

# spark ML 与 MLlib 的区别
- spark.mllib中的算法接口是基于RDDs的；spark.ml中的算法接口是基于DataFrames的。  
技术角度上，面向的数据集类型不一样：ML的API是面向Dataset的（Dataframe是Dataset的子集，也就是Dataset[Row]）， mllib是面对RDD的。Dataset和RDD有啥不一样呢？Dataset的底端是RDD。Dataset对RDD进行了更深一层的优化，比如说有sql语言类似的黑魔法，Dataset支持静态类型分析所以在compile time就能报错，各种combinators（map，foreach等）性能会更好，等等。
- MLlib将仍然支持基于RDD的API spark.mllib并修复错误。
- MLlib不会将新功能添加到基于RDD的API。
- 在Spark 2.x版本中，MLlib将向基于DataFrame的API添加功能，以便与基于RDD的API达成功能对等。
- 达到功能对等（大致估计为Spark 2.2）后，基于RDD的API将被弃用。
- 基于RDD的API预计将在Spark 3.0中被删除。
- DataFrames提供比RDD更友好的API。DataFrame的许多优点包括Spark数据源，SQL / DataFrame查询，Tungsten和Catalyst优化以及跨语言的统一API。
- MLlib的基于DataFrame的API提供跨ML算法和跨多种语言的统一API。
- DataFrames提供比RDD更友好的API便于实际的ML管线，特别是功能转换。
- 基于DataFrame的API，也就是ML模块提倡使用pipelines，把数据想成水，水从管道的一段流入，从另一端流出：
- 大体概念：DataFrame => Pipeline => A new DataFramePipeline: 是由若干个Transformers和Estimators连起来的数据处理过程  
Transformer：入：DataFrame => 出： Data Frame  
Estimator：入：DataFrame => 出：Transformer

- 1

- 1

- 1

- 1

- 1

- 1

- 1

- 1


```python

```
