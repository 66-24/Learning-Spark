# Learning-Spark

## Code 
-  https://github.com/holdenk/spark-testing-base
 -        https://github.com/juarnrh/sscheck
  -       https://github.com/databricks/spark-integration-tests
   -      https://github.com/databricks/spark-perf
    -     https://github.com/holdenk/spark-validator       
- www.scalacheck.org
    
## Testing Framework

```
// to prevent port bind issue in tests        
System.clearProperty("spark.driver.port"); 
        
public class SampleJavaRddTest extends SharedJavaSparkContext 
    implements Serializable {
    
    @Test
    public void verifyMapTest() {
    
        List<Integer> input = Arrays.asList(1,2);
        JavaRDD<Integer> result = sc().parallelize(input)
                        .map(
                        new Function<Integer,Integer>() {
                        
                            public Integer call(Integer x) {
                                return x * x;
                            
                            }
                        
                        };
        assertEquals(input.size(), result.count());                       
    
    }
    
   }
```   
   
# Testing
   - spark-docker / databricks
   - YarnMiniCluster 
   - org.scalatest.scalatest in Java ?

## Using the HiveContext in Testing
 - delete the metastore folder in-between jobs
 - set location for table - else may not have permissions to write to the 
    default location

 # Validate our jobs - How ?
   - Accumulators/Counters - To track number of bad records/no recommendations
   - SimpleHistoricValidation
   - ValidationConf
   
# Talks
  -  Testing Spark Best Procatices 2014
  - Every day I am shuffling data 2015
  - Spark & Spark Streaming Unit Testing
  - Making Spark Unit Testing With Spark Testing Base.  
  - Mastering Spark Unit Testing by Ted Malaska 2016
   
   ```
spakConf.set(spark.broadcase.compress, "false")
spark.shuffle.compress false
spark.shuffle.spill.compress false; 

    val rdd= sqlContext.sparkContext.parallelize(
        Array (
            Row("bob", "1", "1"),
            ...
            )
            
    val userField = new StructField("user", StringType, nullable=true)
    val schema = StructType(Array (userField,...)
    sqlContext.createDataFrame(rdd,schema).registerTempTable("trans")

    val result = RunCountingSql.run(sqlContext)
```
 
