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


01) Read csv file into dataframe :
