# cloud-batch
  This project aims to develop a batch job service for multiple cloud resources. 
Batch Jobs are major style of scientific large data analysis even in the cloud environment. Sometimes, it is required to integrate the legacy local batch jobs in a cluster and the one in the cloud. Furthermore, easy deployment to multiple clouds is important to tackle with rapid increase of the user resource requirement. 

  This cloud batch system consists of 3 major nodes: 1) Scheduler node, 2) Pilot node and 3) Worker nodes. Pilot node and Worker nodes are VM instances in a cloud. The process flow is as followings.

      Users submit a batch job to the Scheduler node with a standard JDL where the local batch
    scheduler is running; SGE in our case. The executable script in this JDL is a special for the cloud:
    cloud-jcontroller.py followed by arguments: real job executable file name, input files et al. ,
    post job script, and environment parameters in the Worker nodes. 
    The cloud-jcontroller.py creates required number of instances in the cloud and call the cloud-jserver.py:
    RPyC deamon which is running in the Pilot node for setting ssh communication with all of the Worker nodes and
    then, initiating the real job script at each node. The completion of jobs are monitored by the cloud-jserver.py,
    the standard output is returned to the Scheduler node after the post job script is finished in the Pilot node. 

      A command line interface is also available in the Scheduler node to test the job interactively.
