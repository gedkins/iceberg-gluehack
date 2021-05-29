Copy this into your project.

You need to specify that you want to use the modified version rather than the original glue catalog. This example is Scala but you can figure out what I mean if you want Java. It also assumes you're using Flink.

```scala
import java.util.HashMap
import org.apache.iceberg.aws.AwsProperties
import org.apache.hadoop.conf.Configuration
import org.apache.iceberg.flink.CatalogLoader


val properties = new HashMap[String,String]
properties.put(AwsProperties.GLUE_CATALOG_ID, "012345678901") // your account number
properties.put("warehouse", "mywarehouse")

// if using dynamodb locking
properties.put("lock-impl", "com.bluecatnetworks.gilesglue.DynamoLockManager")
properties.put("lock.table", "mylocktable")

val catalogLoader = CatalogLoader.custom("iceberg", properties, new Configuration, "com.bluecatnetworks.gilesglue.GlueCatalog")
```
