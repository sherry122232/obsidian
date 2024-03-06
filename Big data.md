## Big data - 1

Hadoop: the definitive guild

![image-20240305121816648](file:///Users/sheyla/Library/Application%20Support/typora-user-images/image-20240305121816648.png?lastModify=1709663519)

### Big data addresses distinct requirements

1. combine multiple unrealated datasets
    
2. process large amounts of unstructured data
    
3. Harvest hidden information in a time-sensitive manner
    

### Terminology

1. a dataset is a collection or group of related data
    
2. Data analysis is the process of examining data to find facts relationships, or trends...
    
3. data analytics: the complete data lifecycle, which encompasses collecting, cleansing, organizing...
    
4. descriptive analytics:
    
    answer questions about events that have already occurrd.
    
5. Diagnostic analytics: determine the cause of a phenomenon that occurred in the apst
    
6. Predictive analytics: aim to determine the outcome of an event that might occur in the future
    
7. Prescriptive analytics build upon the results of predictive analytics by prescribing actions that should be taken
    

### Big data characteristics

1. volume
    
2. velocity
    
3. vriety
    
4. Veracity: quality of data
    

- signal is data that has value and leads to meaningful information

- noise is data taht can't be converted in to information

- registeration: high signal to noise ratio

- blog posting usually have low signal to noise ratio

5. Value: usefulnesss of data for an enterprise
    

value is also impacted by data lifecycle related concerns like how well has the data been stored?

### Different types of data

source: machine/human

format:

1. structured data: conforms to a data model or schema, more often stored in a relational database
    
2. unstructured data:
    
    - textual or binary, like video, image files, audio
        
3. Semi-structured data:
    
    - a defined level of structure and consistency, but is not relational in nature. It is hierarchical or graph-based
        
        - like xml, json, sensor...
            
4. Metadata
    
    - provides information about a dataset's characteristics and structure. it is mostly machine-generated and can be appended to data
        
        - XML tags
            
        - Attributes
            

## Big data - 2
### how can we solve the big data problem?
![[Pasted image 20240305141337.png]]

multiple disk drives are installed in one server, each drive is 2TB - 6TB in size
it is important to match the speed of the drives to the processing power of the server because the CPU can become the bottleneck
### new problem
- how to read the parts of file simultaneously from multiple drives..
- how to find where the pieces if writes to multiple drives...

### Big data storage concepts
1. ==**cluster**==: a tightly coupled collection of servers ("nodes")
	- each node in the cluster has its own dedicated resources, such as memory, a processor and a hard drive
	- a cluster can execute a job by splitting it into small pieces (tasks) and distributing their execution onto different computers that belong to the cluster
2. **==file==**: the most basic unit of storage to store data
	1. a file system is the method of organizing files on a storage device
	2. a distributed file system is a file system that can store large files spread across the nodes of a cluster
3. ==**relational database management system**==: a collection of rows and columns
	1. SQL is used for querying and maintaining the database
4. **==noSQL==**: highly scalable, fault-tolarant and designed to house semi0structured and unstructured data, example:
	- key-value store: redus, dynamo
	- document store: mongoDB, CouchDB
	- wide column store: Bigtable, Hbase, Cassandra
	- graph store: pregel, giraph
5. **Sharding**: is the process of horizontally partitioning 
	- each shard is stored on a separate node, and is responsible for only the data stored on it
	- all shards share the same schema
	- ![[Pasted image 20240305155240.png]]
	- ==how does sharding work==:
		- each shard can independently service reads and writes for the specific subset of data
		- depending on the query, data may need to be fetched from both shards
	- **==benefits==**
		- horizontal scalability
		- provides partial tolerance toward failures, 
	- **==concerns==**
		- queries requiring data from multiple shards
		- data locality -  keeps commonly accessed data co-located on a single shard
	- replication
		- methods: ==master-slave==
			- write to a master node
			- read requests can be fulfilled by any slave node
			- ideal for read intensive loads
			- writes are consistent, while write performance will suffer as the amount of writes increases
			
			- if the master node fails - reads are still possible, write are not supported until reestablished

			- Recovery:
				- resurrect the master node from a backup
				- or choose a new master node from slave
			
			- **Concern**
				- read inconsistency
		- ==peer-to-peer replication ==
			- all nodes operate at the same level
			- each peer is equally capable of handling reads and writes
			- each write is copied to all other peers

			-  concern:
				- write inconsistency - simultaneous update of the same data may happen across multiple peers
			-  strategies:
				- pessimistic concurrency - proactive strategy 
					- locking, ensure there is one update to a record can occur at a time, but this is detrimental to availability
				- optimistic concurrency - reactive strategy 
					- it allows inconsistency to occur ..eventually consistency
		Sharding versus replication - using them both
			![[Pasted image 20240305200812.png]]