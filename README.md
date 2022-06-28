# local standalone Apache Spark

The repository includes the setup of a local standalone cluster of apache spark (3.1.2 version) on a local machine, as well as the execution of basic jobs or tasks to gain a better understanding of working with apache spark in a standalone cluster.

This repository comprises of two sections : 
1. Setup Instructions
2. Execution Instructions by examples

## Setup Instructions

We must first install Apache Spark and any necessary support packages before setting up a standalone cluster on your desktop system.
(https://sparkbyexamples.com/spark/apache-spark-installation-on-windows/)

1. Go to command prompt, run script to start master node:

    <i>bin\spark-class2.cmd org.apache.spark.deploy.master.Master</i>
    <p align="center">
      <img src="https://user-images.githubusercontent.com/96646600/175959775-d89e5d73-48d0-4d55-bdbb-e2d50ddb37ea.jpg">
    </p>
     
   
2. Check on the Console – http://localhost:8080 to ensure Master node is working properly. Look at the web page and there should be something like “spark://localhost.localdomain:7077”

<p align="center">
      <img height= "200" width = "800" src="https://user-images.githubusercontent.com/96646600/175970411-08cfb7e0-29c3-4ce1-8dd0-cc000714395e.jpg">
</p>


3. Go to commmand prompt, run script to start worker node:

    <i>bin\spark-class2.cmd org.apache.spark.deploy.worker.Worker -c 1 -m 4G localhost.localdomain:7077</i>
    <p align = "center">
        <img src = "https://user-images.githubusercontent.com/96646600/175965432-68bc7299-0a4d-49bf-9a59-54ac4f45260b.jpg">
    </p>

    
    

Now you should be able to see an active worker node in the console.
<p align="center">
      <img width="800" src="https://user-images.githubusercontent.com/96646600/175969779-a7d32428-f2c0-4757-9c15-a9a3932ddf8b.jpg">
</p>

## Execution Instructions
We will perform some basic operations with Apache Spark in local standalone instance to gain hands-on experience of working with spark environment. The task listed below is what we'll be working on when executing jobs:

Write pyspark/scala program:
1. Read csv file into dataframe
2. Write the data in the above dataframe to local filesystem in delta format
3. Read the above data written in the delta format into dataframe
4. Show record count for above dataframe

<i>In this section, we will be working on jobs/tasks using command prompt. You can make use of command prompt or other command line interpreter or IDE for executing jobs as per your convenience. </i>

<b> Each task's instructions will be stated clearly, so make sure to follow the steps as directed. </b>

### Operations

As mentioned above, beginning to work on tasks in command prompt, we must run a script (<i>sc.stop()</i>) on command prompt before starting working on tasks in standalone instance. This is because when <i>pyspark</i> is started from a command prompt, a built-in <i>sparkcontext</i> is created, and as a result, working on a standalone cluster will result in an error because only one <i>sparkcontext</i> can be active at a time.

<i> Go to cmd and start with script : \pyspark </i> 

<p align="center">
      <img height = "250" src="https://user-images.githubusercontent.com/96646600/176119601-dc8952b3-a2cf-491a-a743-fcfc8d826522.jpg">
</p>

<i>Now, run cmd with script : \sc.stop() </i>
<p align="center">
      <img height = "150" src="https://user-images.githubusercontent.com/96646600/176121884-5d422b39-dc48-4625-b1b1-cbe59b3aa5ad.jpg">
</p>


#### Working on operations

Task-1) Read csv file into dataframe : In the task we are supposed to read csv file into a dataframe using Apache spark in standalone cluster. In order to run in standalone cluster, we should set<b>master node</b> using <i>url</i> in spark shell, so that <b>worker node</b> can execute the task assigned.
 
 Instructions to set <b>master node</b> in spark shell using command prompt :
 
 1. <i>Go to command prompt, run script:</i>
 
                                     \ from pyspark import SparkConf, SparkContext
                                     \ conf = SparkConf().setAppName(#TaskPredefinedName).setMaster(#urlgeneratedduringsetup)
                                     \ sc = SparkContext(conf=conf)
                                     \ sc
                                     
   <p align = "center">
        <img width = "450" src="https://user-images.githubusercontent.com/96646600/176135779-675689aa-7359-45b8-9146-36e771a6fb33.jpg">
    </p>
                                                                                                                                                                      
                           
                                    
2. <i>Verifying the setup done: </i>
    
   <p align="center">
        <img width = "500" src = "https://user-images.githubusercontent.com/96646600/176138377-6eb57bdf-27f7-4319-8e70-4a23b4ad42a8.jpg">
   </p> 
    
Instructions for executing the task :   
1. <i> Go to command prompt, run script:</i> 
      
       # read csv file into dataframe
       
       \ from pyspak.sql import SparkSession    # introducing sparksession
       \ spark = SparkSession.builder.master(#url).appName(#TaskPredefinedName).getOrCreate() # performing task in standalone cluster
       \ data_f = spark.read.csv(/#file-path.csv , header = True, inferSchema = True)    # reading csv file into spark dataframe
       \ data_f.printSchema()   # schema of dataframe
       
   <p align = "center">
        <img width = "600" src = "https://user-images.githubusercontent.com/96646600/176157351-e68d4539-f4c6-45ba-9ac6-fe6ac1f45ae4.jpg">
    </p>
2. csv file : <i>[link for your reference](https://github.com/SmartyR27/local-spark-standalone/blob/cff7f7ab32a88fb3ca024eb5e23376c03a81da7d/people.csv)</i>
3. Validation of task in master node :
   <p align = "center">
        <img width = "600" src ="https://user-images.githubusercontent.com/96646600/176165506-c4131105-cb63-46ba-9b2c-904af0c25fa7.jpg">
    </p>    

            
Task-2) Write the data in the above dataframe to local filesystem in delta format :

Instructions for executing the task :
1. <i> Go to command prompt, run script:</i> 

       # write the data-dataframe to local filesystem in delta format
       
       \ delta_f = data_f.coalesce(1).write.format("delta").option("header","true").format("csv").save(./filepath)    # saving csv file into local file in delta format
     <p align = "center">
        <img width = "700" src = "https://user-images.githubusercontent.com/96646600/176178998-a3dd0948-cf28-47ca-9d73-44a218978354.jpg">
     </p>

       

2. Validation of task in master node:
 <p align = "center">
        <img width = "600" src ="https://user-images.githubusercontent.com/96646600/176184375-c8cefb19-9199-4864-bbe1-ddfbad623020.jpg">
    </p>
    
    
Task-3) Read the above data written in the delta format into dataframe :

Instructions for executing the task:

1. <i>Go to command prompt, run script:</i>

                    # Read data written in the delta format into dataframe
                    
                    \ r_delta_f = spark.read.format("delta").option("header","true").csv(./filepath)  #spark dataframe
                    \ r_delta_f.show()
                    \ r_delta_f
                    
                    or
                    \ r_delta_f.toPandas()    # pandas dataframe
                    
      <p align = "center">
             <img width = "700" src = "https://user-images.githubusercontent.com/96646600/176195476-c8227e79-2b6e-4eae-84e7-938355187984.jpg">
        </p>
2. Validation of task in master node: 
 <p align = "center">
             <img width = "700" src = "https://user-images.githubusercontent.com/96646600/176196462-1e246095-73ef-4058-8cad-77bb2c98032e.jpg">
    </p>
    
Task-4) Show record count for above dataframe:

Instructions for executing the task:

1. <i>Go to command prompt, run scripts:</i>



