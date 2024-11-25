# Baijan.2

![image](https://github.com/user-attachments/assets/05a1b684-af9f-4eda-8994-fd276ba93bfc)





1. Обновите систему
Откройте терминал и выполните:

sudo apt update
sudo apt upgrade
 
2. Установите Java
Hadoop требует Java. Установите OpenJDK:

sudo apt install openjdk-11-jdk
 
Проверьте версию Java:

java -version
 
3. Создайте пользователя Hadoop
 
sudo adduser hadoop
sudo usermod -aG sudo hadoop
 
Переключитесь на пользователя Hadoop:

su - hadoop
 
4. Скачайте и распакуйте Hadoop
Скачайте последнюю версию Hadoop с официального сайта Apache:

wget https://downloads.apache.org/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz
 
Распакуйте архив:

tar -xvzf hadoop-3.3.6.tar.gz
 
Переместите в удобное место:

sudo mv hadoop-3.3.6 /usr/local/hadoop
 
5. Настройте переменные окружения
Откройте файл .bashrc:

nano ~/.bashrc
 
Добавьте следующие строки в конец файла:

export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
 
Примените изменения:

source ~/.bashrc
 
6. Настройка конфигурационных файлов Hadoop
Отредактируйте следующие файлы:

core-site.xml:

<configuration>
 <property>
   <name>fs.defaultFS</name>
   <value>hdfs://localhost:9000</value>
 </property>
</configuration>
● Файл расположен в /usr/local/hadoop/etc/hadoop/core-site.xml.
hdfs-site.xml:

<configuration>
 <property>
   <name>dfs.replication</name>
   <value>1</value>
 </property>
 <property>
   <name>dfs.namenode.name.dir</name>
   <value>file:///usr/local/hadoop/hadoopdata/hdfs/namenode</value>
 </property>
 <property>
   <name>dfs.datanode.data.dir</name>
   <value>file:///usr/local/hadoop/hadoopdata/hdfs/datanode</value>
 </property>
</configuration>
●
Создайте каталоги для NameNode и DataNode:

mkdir -p /usr/local/hadoop/hadoopdata/hdfs/namenode
mkdir -p /usr/local/hadoop/hadoopdata/hdfs/datanode
 
7. Форматирование HDFS
hdfs namenode -format
 
8. Запуск Hadoop
Запустите NameNode и DataNode:

start-dfs.sh
 
Проверьте работу Hadoop:

jps
 
Для остановки Hadoop используйте:

stop-dfs.sh
 
 
