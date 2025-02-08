
### **a) User-Defined Function (UDF) in Hive to Convert Strings to Uppercase**
Hive allows creating custom UDFs using Java. Below is a simple Java-based UDF to convert a string to uppercase:

```java
import org.apache.hadoop.hive.ql.exec.UDF;
import org.apache.hadoop.io.Text;

public class ToUpperCaseUDF extends UDF {
    public Text evaluate(Text input) {
        if (input == null) {
            return null;
        }
        return new Text(input.toString().toUpperCase());
    }
}
```

**Steps to Use:**
1. Compile the Java file and create a JAR.
2. Add the JAR in Hive:
   ```sql
   ADD JAR /path/to/your-udf.jar;
   CREATE TEMPORARY FUNCTION to_upper AS 'ToUpperCaseUDF';
   ```
3. Use it in Hive:
   ```sql
   SELECT to_upper(name) FROM employees;
   ```

---

### **b) Reading a File from Hadoop File System (HDFS) using Java**
This Java program reads a file from HDFS and prints its content.

```java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import java.io.*;

public class ReadHDFSFile {
    public static void main(String[] args) throws IOException {
        String hdfsFilePath = "hdfs://localhost:9000/user/data/sample.txt"; // Change as per your setup

        Configuration conf = new Configuration();
        FileSystem fs = FileSystem.get(conf);
        Path path = new Path(hdfsFilePath);
        BufferedReader br = new BufferedReader(new InputStreamReader(fs.open(path)));

        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }

        br.close();
        fs.close();
    }
}
```

**Steps to Use:**
1. Set up Hadoop and ensure HDFS is running.
2. Compile and run the Java program.

---

These programs are simple yet effective solutions for working with Hive UDFs and Hadoop HDFS. Let me know if you need modifications! 🚀
