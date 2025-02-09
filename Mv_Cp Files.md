
### **HDFS Commands for Moving and Copying Files**
Instead of Java, HDFS provides built-in commands to **move and copy files within HDFS**.

### **Move a File**
```sh
hdfs dfs -mv /user/data/file1.txt /user/archive/
```

### **Copy a File**
```sh
hdfs dfs -cp /user/data/file1.txt /user/backup/
```

### **Move a Directory**
```sh
hdfs dfs -mv /user/data /user/processed_data
```

### **Copy a Directory**
```sh
hdfs dfs -cp /user/data /user/backup_data
```

### **Upload (Put) a File into HDFS**
```sh
hdfs dfs -put localfile.txt /user/hadoop/
```
- Uploads `localfile.txt` from the local system to the HDFS directory `/user/hadoop/`.  

---

### **Copy a File from Local to HDFS**
```sh
hdfs dfs -copyFromLocal localfile.txt /user/hadoop/
```
- Similar to `put`, but used specifically for copying from local to HDFS.  

---

### **Move a File within HDFS**
```sh
hdfs dfs -mv /user/hadoop/localfile.txt /user/hadoop/newfile.txt
```
- Moves or renames a file in HDFS.  

---

### **Copy a File within HDFS**
```sh
hdfs dfs -cp /user/hadoop/localfile.txt /user/hadoop/copyfile.txt
```
- Copies `localfile.txt` to `copyfile.txt` in the same directory.
  
---

### **Copy a File from HDFS to Local**
```sh
hdfs dfs -copyToLocal /user/hadoop/localfile.txt /home/user/
```
- Copies `localfile.txt` from HDFS to the local directory `/home/user/`.  
