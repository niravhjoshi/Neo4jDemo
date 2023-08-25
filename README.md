
Please find following assighment request:

 - Set up Neo4j Enterprise (Docker / VM).
		

>  1. I have setup docker on my machine installed as Docker Desktop. 		
>  2. I went through Neo4j site in download section they have mention docker hub link where Neo4j hosting docker repos.(https://hub.docker.com/_/neo4j)
>  3. Using following docker command we have starte docker container for Neo4j and command has following parts where it expose storage of host($Home/neo4j/data) at mount point of container(/data)

`docker run --publish=7474:7474 --publish=7687:7687 --volume=$HOME/neo4j/data:/data  --env=NEO4J_ACCEPT_LICENSE_AGREEMENT=yes neo4j:4.4.24-enterprise`

>  4.Please find above command output as following
 
`➜  ~ docker run --publish=7474:7474 --publish=7687:7687 --volume=$HOME/neo4j/data:/data  --env=NEO4J_ACCEPT_LICENSE_AGREEMENT=yes neo4j:4.4.24-enterprise                                                          [23/08/15| 3:11PM]
Warning: Folder mounted to "/data/transactions" is not writable from inside container. Changing folder owner to neo4j.
2023-08-15 09:41:24.923+0000 INFO  Starting...
2023-08-15 09:41:25.569+0000 INFO  This instance is ServerId{a6c136f4} (a6c136f4-cf39-4a3c-8008-a489411dba7d)
2023-08-15 09:41:27.908+0000 INFO  ======== Neo4j 4.4.24 ========
2023-08-15 09:41:30.748+0000 INFO  Sending metrics to CSV file at /var/lib/neo4j/metrics
2023-08-15 09:41:30.905+0000 INFO  Bolt enabled on 0.0.0.0:7687.
2023-08-15 09:41:32.444+0000 INFO  Remote interface available at http://localhost:7474/
2023-08-15 09:41:32.452+0000 INFO  id: 29FC01BC6B479506E5AC054740CE9A60624FAAFA2B37BF81D5D804A9609E1BD9
2023-08-15 09:41:32.452+0000 INFO  name: system
2023-08-15 09:41:32.453+0000 INFO  creationDate: 2023-08-14T18:06:22.282Z
2023-08-15 09:41:32.454+0000 INFO  Started.`

>  5.Above command also expose two port from container to host 7474 is http port where we can connect to Ne04j using browser and bolt protocol is enable on port number 7687 host can connect to Neo4j application using port number 7687


 - Model any of the below datasets from Tabular to Graph using arrows.app and share the JSON export or URL of the data model.
  1. We have created model for Bankdata where it has customers,transfers and purchases data in it.
   
  2. Here is Relation model for Bankdata for reference purpose we have created.
     Please refer to this image 
     [[/image/bankDBRelationShip.ejpgxt|ALT TEXT]]
  3. Here is Graph Model derived for Bankdata in arrows App.
    https://drive.google.com/file/d/1R6jbv7EBePvmqsjAPNV0lD0xkZfv7xnr/view?usp=sharing
- Write a graph-enabled application using JavaScript / Python / Go / .Net / Java to ingest data based on the data model.
  1. Please find file name Neo4JDataLoad.ipynb which has python code to ingest data for sng_education.
   
 - Write some exploratory Cypher queries to look at some patterns. 
    
    `   
	MATCH (w:Work),(tr:Trips)
	where w.passportnumber = tr.passportnumber
	CREATE (w) -[r:Perform_Trips]-> (tr)
	return w,tr,r


	MATCH (w:Work),(ed:Education)
	where w.passportnumber = ed.passportnumber
	CREATE (w) -[r:had_study_in] ->(ed)
	return w,ed,r

	MATCH (w:Work),(tr:Transaction)
	where w.passportnumber = tr.passportnumber
	CREATE (w) -[r:has_performed_transaction] ->(tr)
	return w,tr,r
`
