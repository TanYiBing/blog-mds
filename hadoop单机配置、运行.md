---
title: hadoop单机安装、运行
date: 2017-12-28 22:28:13
update:
tags: [hadoop,java,VMware,Windows]
categories: hadoop
---
# 云计算
![hadoop](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1513179599832&di=5338ae758687dfbf1514313e6c522592&imgtype=0&src=http%3A%2F%2Fimages2015.cnblogs.com%2Fblog%2F793015%2F201611%2F793015-20161127231256315-1152955812.png)

## 配置步骤

**Tanyibing**，this is for *14级软件工程专业*，*My email <tanyibing1995@gmail.com> link* 

### Hadoop环境准备工作
* **VMware版本VMware-workstation-full-12.5.7-5813279(版本自己选择)Xshell5自己选择是否使用**
* **CentOS版本CentOS-6.4-x86_64-bin-DVD1(本人的是64位，其他版本未测试)**
* **Hadoop版本hadoop-2.6.0(安装完系统后直接命令行安装)**
* **jdk版本jdk-8u45-linux-x64.tar**
* **需要了解基本的linux和vim的使用**

### 资源位置
**百度网盘:[https://pan.baidu.com/s/1i5s2eFF](https://pan.baidu.com/s/1i5s2eFF)**
**密码:n3jq**

**CentOS镜像下载地址[http://mirror.nsc.liu.se/centos-store/6.4/isos/x86_64/](http://mirror.nsc.liu.se/centos-store/6.4/isos/x86_64/)**

## VMware安装以及CentOS安装

### VMware安装步骤省略
### CentOS安装
1.点击新建虚拟机
>![](/img/2017-12-20-hadoop单机配置、运行/1.png)

2.选择稍后操作系统
>![](/img/2017-12-20-hadoop单机配置、运行/2.png)

3.选择64位CentOS的系统
>![](/img/2017-12-20-hadoop单机配置、运行/3.png)

4.选择安装位置(最好不要放C盘)
>![](/img/2017-12-20-hadoop单机配置、运行/4.png)

5.默认配置就好，点击下一步
>![](/img/2017-12-20-hadoop单机配置、运行/5.png)

6.点击自定义硬件
>![](/img/2017-12-20-hadoop单机配置、运行/6.png)

7.配置虚拟机的内存，我们的实验1G即可，电脑好的选择2G也可
>![](/img/2017-12-20-hadoop单机配置、运行/7.png)

8.选择虚拟化cpu(使用本机真实cpu)
>![](/img/2017-12-20-hadoop单机配置、运行/8.png)

9.选择加载的镜像，选1盘，如果自己下载的话2盘是一些软件，不需要加载
>![](/img/2017-12-20-hadoop单机配置、运行/9.png)

10.**桥接和NAT模式才能上网，我选择的是桥接(使用自己的真实网卡)**
>![](/img/2017-12-20-hadoop单机配置、运行/10.png)

11.选择第一个选项(安装或升级系统)
>![](/img/2017-12-20-hadoop单机配置、运行/11.png)

12.这一步选skip跳过即可
>![](/img/2017-12-20-hadoop单机配置、运行/12.png)

13.选择简体中文，点击下一步
>![](/img/2017-12-20-hadoop单机配置、运行/13.png)

14.选择英国美式，下一步
>![](/img/2017-12-20-hadoop单机配置、运行/14.png)

15.选择默认的基本存储设备，下一步
>![](/img/2017-12-20-hadoop单机配置、运行/15.png)

16.**必须选择是，忽略所有数据**
>![](/img/2017-12-20-hadoop单机配置、运行/16.png)

17.默认就行，下一步
>![](/img/2017-12-20-hadoop单机配置、运行/17.png)

18.自己输入密码（6位，字母数字），选择无论如何使用(因为我设置的密码不是安全的)
>![](/img/2017-12-20-hadoop单机配置、运行/18.png)

19.为了更好的了解linux，现在进行分盘(挂载点)
>![](/img/2017-12-20-hadoop单机配置、运行/19.png)

20.首先分给/home 2G(选择空闲点击创建，然后挂载点选/home)
>![](/img/2017-12-20-hadoop单机配置、运行/20.png)

21.必须给/boot一定的空间(系统使用，及时其他出现问题也能正常开机，一般200M即可)
>![](/img/2017-12-20-hadoop单机配置、运行/21.png)

22.接着给swap分4G空间(不是在挂载点选择，而是在文件系统类型选择)
>![](/img/2017-12-20-hadoop单机配置、运行/22.png)

23.最后所有空间都分给 / 挂载点(根目录)
>![](/img/2017-12-20-hadoop单机配置、运行/23.png)

24.选择将修改写入磁盘，点击下一步
>![](/img/2017-12-20-hadoop单机配置、运行/24.png)

25.默认即可，下一步
>![](/img/2017-12-20-hadoop单机配置、运行/25.png)

26.由于minimal存在一些兼容问题，选择Basic Server版本，点击下一步进行安装
>![](/img/2017-12-20-hadoop单机配置、运行/26.png)

27.安装完成，点击重新引导，重启虚拟机
>![](/img/2017-12-20-hadoop单机配置、运行/27.png)

28.先输入用户名：root 回车，接着输入密码(密码是不显示的，输入完回车就行)
>![](/img/2017-12-20-hadoop单机配置、运行/28.png)

29.现在一个虚拟机就终于安装完成了

## jdk、hadoop的解压

**1.将jdk解压到 /opt 下**

>     tar -zxvf jdk-8u45-linux-x64.tar.gz -C /opt

*注意如果你的虚拟机自带openjdk需要先卸载*

>     rpm -qa | grep java //检查机器上的jdk

应该显示这一类的结果：

>     java-1.8.0-openjdk-1.8.0.102-4.b14.el7.x86_64
>     javapackages-tools-3.4.1-11.el7.noarch
>     java-1.8.0-openjdk-headless-1.8.0.102-4.b14.el7.x86_64

使用下面的命令删除上面列出的内容：

>     rpm -e --nodeps + 上面出现的内容



**2.将hadoop解压到 /opt/hadoop 下**

>     tar -zxvf hadoop-2.6.0-x64.tar.gz -C /opt/hadoop
*没有hadoop目录的自己在/opt下创建*

在/root /hadoop/目录下，建立tmp、hdfs/name、hdfs/data目录，执行如下命令：
>     mkdir /opt/hadoop/tmp 
>     mkdir /opt/hadoop/hdfs 
>     mkdir /opt/hadoop/hdfs/data 
>     mkdir /opt/hadoop/hdfs/name 

##ssh的安装、无密码配置

**1.检查**

CentOS 默认已安装了 SSH client、SSH server，打开终端执行如下命令进行检验：

>     rpm -qa | grep ssh 

成功显示出client、server版本的话则无需安装，若需要安装，则可以通过 yum 进行安装（安装过程中会让你输入 [y/N]，输入 y 即可）：

>     sudo yum install openssh-clients
>     sudo yum install openssh-server

接着执行如下命令测试一下 SSH 是否可用：

>     ssh localhost

此时会有提示(SSH首次登陆提示)，输入 yes 。然后按提示输入密码，就登陆到本机了。

**2.ssh无密码配置**

上面这样登陆是需要每次输入密码的，我们需要配置成SSH无密码登陆比较方便。

首先输入 exit 退出刚才的 ssh，就回到了我们原先的终端窗口，然后利用 ssh-keygen 生成密钥，并将密钥加入到授权中：

>     exit                           # 退出刚才的 ssh localhost
>     cd ~/.ssh/                     # 若没有该目录，请先执行一次ssh localhost
>     ssh-keygen -t rsa              # 会有提示，都按回车就可以
>     cat id_rsa.pub >> authorized_keys  # 加入授权
>     chmod 600 ./authorized_keys    # 修改文件权限

此时再用 ssh localhost 命令，无需输入密码就可以直接登陆了。

## jdk、hadoop的配置

**1.环境变量的配置**

>     vim /etc/profile加入如下配置：     
>     export JAVA_HOME=/opt/jdk1.8.0_45
>     export HADOOP_HOME=/opt/hadoop/hadoop-2.6.0
>     exportCLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:
>     exportPATH=$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:

保存后，不要忘记执行如下命令使配置生效：
>     source /etc/profile

**2.hosts文件的修改**

>     vim /etc/hosts最后加入如下内容：
>     127.0.0.1    自己的主机名

**3.hadoop配置**

进入/opt/hadoop/hadoop-2.6.0/etc/hadoop目录

##### 1)在hadoop-env.sh和 yarn-env.sh的开头添加如下环境变量(一定要添加) 
>     export JAVA_HOME=/opt/jdk1.8.0_45 

##### 2)配置core-site.xml  
>     <configuration>
>     	<property>
>     		<name>fs.default.name</name>
>     		<value>hdfs://localhost:9000</value>
>     		<description>HDFS的URI，文件系统://namenode标识:端口号</description>
>     	</property>
>     	<property>
>     		<name>hadoop.tmp.dir</name>
>     		<value>/opt/hadoop/tmp</value>
>     		<description>namenode上本地的hadoop临时文件夹</description>
>     	</property>
>     </configuration>

##### 3)配置hdfs-site.xml 
>     <configuration>
>     	<!—hdfs-site.xml-->
>     	<property>
>     		<name>dfs.name.dir</name>
>     		<value>/opt/hadoop/hdfs/name</value>
>     		<description>namenode上存储hdfs名字空间元数据 </descriptio>     	 
>     	</property>
>     	<property>
>     		<name>dfs.data.dir</name>
>     		<value>/opt/hadoop/hdfs/data</value>
>     		<description>datanode上数据块的物理存储位置</description>
>     	</property>
>     	<property>
>     		<name>dfs.replication</name>
>     		<value>1</value>
>     		<description>副本个数，配置默认是3,应小于datanode机器数量</description>
>     	</property>
>     </configuration>

##### 4)配置yarn-site.xml 
>     <configuration>
>     	<property>
>     		<name>yarn.nodemanager.aux-services</name>
>     		<value>mapreduce_shuffle</value>
>     	</property>
>     	<property>
>     		<name>yarn.resourcemanager.webapp.address</name>
>     		<value>${yarn.resourcemanager.hostname}:8099</value>
>     	</propert>     
>     </configuration>

#####4)配置mapred-site.xml 

目录下没有mapred-site.xml，只有mapred-site.xml.template(模板)，所以将其复制重命名为mapred-site.xml:
>     cp mapred-site.xml.template mapred-site.xml

然后再配置mapred-site.xml:
>     <configuration>
>     	<property>
>     		<name>mapreduce.framework.name</name>
>     		<value>yarn</value>
>     	</property>
>     </configuration>

##### 5)配置yarn-site.xml 
>     <configuration>
>     	<property>
>     		<name>yarn.nodemanager.aux-services</name>
>     		<value>mapreduce_shuffle</value>
>     	</property>
>     	<property>
>     		<name>yarn.resourcemanager.webapp.address</name>
>     		<value>${yarn.resourcemanager.hostname}:8099</value>
>     	</property>
>     </configuration>

## 启动hadoop

**1.格式化namenode**
>     hadoop namenode -format

**2.启动hadoop**
>     start-all.sh

**3.启动验证**
>     jps
应该输出如下的结果:

>![](/img/2017-12-20-hadoop单机配置、运行/29.png)

在浏览器输入虚拟机的ip地址，例如：192.168.31.0:50070，能够打开如下网页：
>![](/img/2017-12-20-hadoop单机配置、运行/30.png)

***至此，hadoop环境安装已经全部完成***

## ***hadoop下运行MapReduce代码***

**在此，使用WordCount的旧版api版本演示**

**1.编写WordCount.java,包含Mapper类和Reducec类**
>     import java.io.IOException;
>     import java.util.StringTokenizer;
>     import org.apache.hadoop.conf.Configuration;
>     import org.apache.hadoop.fs.Path;
>     import org.apache.hadoop.io.IntWritable;
>     import org.apache.hadoop.io.LongWritable;
>     import org.apache.hadoop.io.Text;
>     import org.apache.hadoop.mapreduce.Job;
>     import org.apache.hadoop.mapreduce.Mapper;
>     import org.apache.hadoop.mapreduce.Reducer;
>     import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
>     import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
>     import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
>     import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;
>     public class WordCount {
>		public static class WordCountMap extends
>				Mapper<LongWritable, Text, Text, IntWritable> {
>			private final IntWritable one = new IntWritable(1);
>			private Text word = new Text();
>			public void map(LongWritable key, Text value, Context context)
>					throws IOException, InterruptedException {
>				String line = value.toString();
>				StringTokenizer token = new StringTokenizer(line);
>				while (token.hasMoreTokens()) {
>					word.set(token.nextToken());
>					context.write(word, one);
>				}
>			}
>		}
>		public static class WordCountReduce extends
>				Reducer<Text, IntWritable, Text, IntWritable> {
>			public void reduce(Text key, Iterable<IntWritable> values,
>					Context context) throws IOException, InterruptedException {
>				int sum = 0;
>				for (IntWritable val : values) {
>					sum += val.get();
>				}
>				context.write(key, new IntWritable(sum));
>			}
>		}
>		public static void main(String[] args) throws Exception {
>			Configuration conf = new Configuration();
>			Job job = new Job(conf);
>			job.setJarByClass(WordCount.class);
>			job.setJobName("wordcount");
>			job.setOutputKeyClass(Text.class);
>			job.setOutputValueClass(IntWritable.class);
>			job.setMapperClass(WordCountMap.class);
>			job.setReducerClass(WordCountReduce.class);
>			job.setInputFormatClass(TextInputFormat.class);
>			job.setOutputFormatClass(TextOutputFormat.class);
>			FileInputFormat.addInputPath(job, new Path(args[0]));
>			FileOutputFormat.setOutputPath(job, new Path(args[1]));
>			job.waitForCompletion(true);
>		}
>     }


**2.编译WordCount.java文件**
>javac WordCount.java -d 指定到你希望的目录下

此时目录下应该多出三个文件：_WordCount.class_、_WordCount$WordCountMap.class_、WordCount$WordCountReduce.class

**3.将以上的.class文件打包成.Jar文件**
>     jar -cvf 你希望指定的名字.jar *.class


**4.创建hadoop的input和output目录**
>     hadoop fs -mkdir input
>     hadoop fs -mkdir output

**5.将要输入的文件放进input目录下**
>     hadoop fs -put 你要放入计算的文件 input

**6.hadoop运行Jar文件并计算结果**
>     hadoop jar WordCount.Jar WordCount input/file output
>     (hadoop jar jar包路径 执行的主函数名(主类名，main方法所在类名) 输入目录名 输出目录名)


**7.查看结果(前提是不报错，成功运行完)**

成功的话，output目录下会出现一个part-r-xxxx
>     hadoop fs cat output/part-r-00000 #查看提交的结果


## 附(xshell5、VMware tools使用安装)


***VMware Tools可以让虚拟机和你的主机之间共享一个文件夹,具体操作不在此赘述，点击链接自行按教程安装[VMware Tools安装](https://jingyan.baidu.com/article/8ebacdf070c40c49f75cd558.html)***

***Xshell可以方便开发,具体操作不在此赘述，点击链接自行按教程安装[Xshell安装](http://blog.csdn.net/white_gs/article/details/52263365)***