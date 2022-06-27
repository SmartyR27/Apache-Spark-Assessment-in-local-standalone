# local standalone Apache Spark

The repository includes the setup of a local standalone cluster of apache spark (3.1.2 version) on a local machine, as well as the execution of basic jobs or tasks to gain a better understanding of working with apache spark in a standalone cluster.

This repository comprises of two sections : 
1. Setup Instructions
2. Execution Instructions with task examples

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
