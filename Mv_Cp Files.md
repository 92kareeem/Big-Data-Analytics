
### **HDFS Commands for Moving and Copying Files**
Instead of Java, HDFS provides built-in commands to **move and copy files within HDFS**.

#### **Move a File**
```sh
hdfs dfs -mv /user/data/file1.txt /user/archive/
```

#### **Copy a File**
```sh
hdfs dfs -cp /user/data/file1.txt /user/backup/
```

#### **Move a Directory**
```sh
hdfs dfs -mv /user/data /user/processed_data
```

#### **Copy a Directory**
```sh
hdfs dfs -cp /user/data /user/backup_data
```
