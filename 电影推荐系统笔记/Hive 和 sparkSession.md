## Hive 和 sparkSession

#### 1 Hive在sparkSession中



```java
class SingleSparkSession() {
  /**
   * 在windows客户端命名，否则在hdfs中没有权限
   */
  System.setProperty("HADOOP_USER_NAME", "linrushao")

  val sparkConf = new SparkConf().setAppName("StreamingRecommender").setMaster("local[*]")

  val spark = SparkSession.builder()
    .config(sparkConf)
    .appName("StreamingRecommender")
    .master("local[*]")
    .enableHiveSupport()
    .getOrCreate()
 }
}
```

想要利用sparksession在excuter端创建hive支持，发现不符合spark的设计原理，导致在excutor端无法使用sparksession

 * 也就是说sparksession是在driver端运行的，所以只有在driver端才能连接hive，才可以利用hive查询语句，在excutor端要想获取driver端数据
 * 虽然可以通过广播方法把少量数据缓存咋excutor端，但是后期我们要对hive表进行更新语句操作，所以通过广播方式虽然可以达到查询对比的效果
 * 但是后面的操作我们无法完成或者比较困难，所以这时候我们就可以利用mongodb数据库库进行操作，将数据存入到mongodb数据库中

### 2 尝试利用单例模式

就是直接创建一个单独的Spark Session对象，在需要利用的时候直接调用方法

```java
object SingleSparkSession {
  private val demo = new SingleSparkSession
  def getContext(): SingleSparkSession = {
    demo
  }
```

因为在上述的问题中就是说明在ratingStream.foreachRDD不支持传SparkSession值，所以设置才里面直接嗲用新得对象，发现并不可取