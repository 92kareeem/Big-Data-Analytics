### **Word Count Application Using Hadoop MapReduce (Single Java File)**  
Here’s a **single-block Java program** for Word Count using Hadoop MapReduce:

```java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import java.io.IOException;
import java.util.StringTokenizer;

public class WordCount {
    
    // Mapper Class
    public static class TokenizerMapper extends Mapper<Object, Text, Text, IntWritable> {
        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
                word.set(itr.nextToken());
                context.write(word, one);
            }
        }
    }

    // Reducer Class
    public static class IntSumReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
        public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
                sum += val.get();
            }
            context.write(key, new IntWritable(sum));
        }
    }

    // Driver Class (Main Method)
    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "word count");

        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);

        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);

        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```
1. hadoop fs -put Desktop/INPUT.txt
2. hadoop jar WORDCOUNT.jar WORDCOUNT.WORDCOUNT INPUT.txt dir7

---

## **Execution Steps in Cloudera VirtualBox**
Follow these steps to run the Word Count program inside **Cloudera VirtualBox**.

### **1. Start Cloudera VM and Hadoop Services**
   - Open **Cloudera VirtualBox**.
   - Start Hadoop by running:
     ```sh
     start-all.sh
     ```

---

### **2. Create Input and Output Directories in HDFS**
   - Open the terminal and create an input directory:
     ```sh
     hdfs dfs -mkdir -p /user/cloudera/input
     ```
   - Upload a sample text file to HDFS:
     ```sh
     hdfs dfs -put sample.txt /user/cloudera/input/
     ```

---

### **3. Compile and Package the Word Count Program**
   - **Compile the program** using Hadoop’s classpath:
     ```sh
     javac -classpath `hadoop classpath` -d . WordCount.java
     ```
   - **Create a JAR file**:
     ```sh
     jar -cvf wordcount.jar *.class
     ```

---

### **4. Run the Hadoop Job**
   - Execute the program with input and output paths:
     ```sh
     hadoop jar wordcount.jar WordCount /user/cloudera/input /user/cloudera/output
     ```

---

### **5. View the Output**
   - Check if the output directory is created:
     ```sh
     hdfs dfs -ls /user/cloudera/output
     ```
   - Display the word count results:
     ```sh
     hdfs dfs -cat /user/cloudera/output/part-r-00000
     ```

---

## **Execution Steps in Eclipse**
### **1. Set Up Hadoop in Eclipse**
   - Install **Eclipse IDE**.
   - Install **Hadoop Plugin** (if needed).
   - Add **Hadoop Libraries** to the project (JAR files from `hadoop-*/lib`).

### **2. Create a New Java Project**
   - Open **Eclipse** → **File** → **New** → **Java Project**.
   - Name it `HadoopWordCount`.
   - Add **WordCount.java** to `src`.

### **3. Configure Hadoop Dependencies**
   - Right-click the project → **Properties** → **Java Build Path**.
   - Add External JARs from Hadoop (`hadoop-core.jar`, etc.).

### **4. Export as JAR File**
   - Right-click **HadoopWordCount** → **Export** → **JAR File**.
   - Save as `wordcount.jar`.

### **5. Transfer JAR to Cloudera VM**
   - Move the `wordcount.jar` to Cloudera using SCP or a shared folder.

### **6. Run the Program on Hadoop**
   - Follow the same execution steps as in Cloudera VirtualBox.

---

## **Final Output Example**
```
hello    4
world    2
hadoop   3
bigdata  1
```

Now, you have a complete **Word Count MapReduce program**, along with **execution steps in Cloudera VirtualBox and Eclipse**. 🚀 Let me know if you need any modifications!
