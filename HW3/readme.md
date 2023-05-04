# ECE530 HW3-report

Name: Yie-Sheng Chen
ID: 
e-mail: 

## Introduction

In this HW3, I mainly followed the 2015 medium.com post, "Deploy a MongoDB Cluster in 9 easy steps Using Docker", "Docker: Up & Running" by Sean P. Kane with Karl Matthias and a mongodb book, "MongoDB Recipes With Data Modeling and Query Building Strategies-Apress (2020)".

Similar to HW1, I think the most difficult part is to grasp to general idea and direction of the homework requirement. This is difficult because, without background knowledge, it's easy to make mistake, skip steps, and then at a loss as to how to go back and how to restore the system to the clean state. For example, when testing mongodb functionality, I didn't realize, in addition to removing the old container, I also needed to remove the data directory.

I solved this HW3 in the following sequence:
1. setting up the environment: using Vagrant to start 3 basic Ubuntu 20 Virtualbox virtual machines.
2. directly ran the commands on the medium.com post which means pulling the  mongodb version 2.6 from the Internet.
3. In case mongodb changed too much in the newer version, I managed to find the Dockerfile of mongodb 2.6 and tried to "docker build" from it. I solved some errors by modifying the Dockerfile but, in the end, cannot solve "gpg keyserver" error.
4. I tried newer mongodb Dockerfile, specifically: https://github.com/docker-library/mongo/blob/685ebea/4.2/Dockerfile and solved some subsequent minor errors:  missing "docker-entrypoint.sh", "chmod +x docker-entrypoint.sh", "chmod 600" the mongodb-keyfile and etc. 
5. Study necessary mongodb functionalities: create, query, and access data on secondary mongodb instance.
6. Find out how to start an empty mongodb.

## Troubleshooting processes
Details are listed in the following deployment steps and includes the following items:
* update Vagrantfiles
* choose suitable mongodb version
* how to start empty mongodb

## Deployment steps, commands, console outputs and screenshots

### setting up environment
#### use vagrant to start Virtualbox VMs
```
$ vagrant up
```

#### inside Virtualbox VMs: on node1/2/3
```
# apt-get remove docker docker.io containerd runc
# apt-get remove docker-engine
# apt-get update
# apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
# mkdir -p /etc/apt/keyrings
# curl -fsSL https://download.docker.com/linux/ubuntu/gpg |\
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
# chmod a+r /etc/apt/keyrings/docker.gpg
# echo \
    "deb [arch=$(dpkg --print-architecture) \
    signed-by=/etc/apt/keyrings/docker.gpg] \
    https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" |\
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
# apt-get update
# apt-get install \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    docker-compose-plugin

Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.20) ...

# docker --version
Docker version 23.0.5, build bc4487a

```
* Sean P. Kane with Karl Matthias, "Docker: Up & Running", 2023

### Docker build on primary and scp to secondary mongodb containers

#### docker build on node1
```
# mkdir mongo42
# cd mongo42
# vim Dockerfile
# vim docker-entrypoint.sh
# docker build --tag mongo .
[+] Building 89.9s (14/14) FINISHED                                                                                                                                         
 => [internal] load build definition from Dockerfile                                                                                                                   0.0s
 => => transferring dockerfile: 4.07kB                                                                                                                                 0.0s
 => [internal] load .dockerignore                                                                                                                                      0.0s
 => => transferring context: 2B                                                                                                                                        0.0s
 => [internal] load metadata for docker.io/library/ubuntu:bionic                                                                                                       1.8s
 => [1/9] FROM docker.io/library/ubuntu:bionic@sha256:8aa9c2798215f99544d1ce7439ea9c3a6dfd82de607da1cec3a8a2fae005931b                                                 3.5s
 => => resolve docker.io/library/ubuntu:bionic@sha256:8aa9c2798215f99544d1ce7439ea9c3a6dfd82de607da1cec3a8a2fae005931b                                                 0.0s
 => => sha256:8aa9c2798215f99544d1ce7439ea9c3a6dfd82de607da1cec3a8a2fae005931b 1.33kB / 1.33kB                                                                         0.0s
 => => sha256:0779371f96205678dbcaa3ef499be2e5f262c8b09aadc11754bf3daf9f35e03e 424B / 424B                                                                             0.0s
 => => sha256:3941d3b032a8168d53508410a67baad120a563df67a7959565a30a1cb2114731 2.30kB / 2.30kB                                                                         0.0s
 => => sha256:0c5227665c11379f79e9da3d3e4f1724f9316b87d259ac0131628ca1b923a392 25.69MB / 25.69MB                                                                       2.9s
 => => extracting sha256:0c5227665c11379f79e9da3d3e4f1724f9316b87d259ac0131628ca1b923a392                                                                              0.5s
 => [internal] load build context                                                                                                                                      0.0s
 => => transferring context: 14.28kB                                                                                                                                   0.0s
 => [2/9] RUN set -eux;  groupadd --gid 999 --system mongodb;  useradd --uid 999 --system --gid mongodb --home-dir /data/db mongodb;  mkdir -p /data/db /data/configd  0.4s
 => [3/9] RUN set -eux;  apt-get update;  apt-get install -y --no-install-recommends   ca-certificates   gnupg   jq   numactl   procps  ;  rm -rf /var/lib/apt/lists  14.4s 
 => [4/9] RUN set -ex;   savedAptMark="$(apt-mark showmanual)";  apt-get update;  apt-get install -y --no-install-recommends   wget  ;  rm -rf /var/lib/apt/lists/*;  23.5s 
 => [5/9] RUN mkdir /docker-entrypoint-initdb.d                                                                                                                        0.3s 
 => [6/9] RUN set -ex;  export GNUPGHOME="$(mktemp -d)";  set -- 'E162F504A20CDF15827F718D4B7C549A058F8B6B';  for key; do   gpg --batch --keyserver keyserver.ubuntu  21.2s 
 => [7/9] RUN echo "deb [ signed-by=/etc/apt/keyrings/mongodb.gpg ] http://$MONGO_REPO/apt/ubuntu bionic/${MONGO_PACKAGE%-unstable}/$MONGO_MAJOR multiverse" | tee "/  0.3s 
 => [8/9] RUN set -x  && export DEBIAN_FRONTEND=noninteractive  && apt-get update  && apt-get install -y   mongodb-org=4.2.24   mongodb-org-server=4.2.24   mongodb-  23.2s 
 => [9/9] COPY docker-entrypoint.sh /usr/local/bin/                                                                                                                    0.0s 
 => exporting to image                                                                                                                                                 1.3s 
 => => exporting layers                                                                                                                                                1.3s 
 => => writing image sha256:9970b5d215b5984e3c3f240316530786491cc8f4c0c83de0640a5408726c3398                                                                           0.0s 
 => => naming to docker.io/library/mongo
```

![](https://i.imgur.com/LNY4aGg.png)

```
docker run --name mongo -v /home/core/mongo-files/data:/data/db -v /home/core/mongo-files:/opt/keyfile --hostname="node1.example.com" -p 27017:27017 -d mongo  --smallfiles
a147ac506a785e8abe1c9e0b2d6abde3d0fa0241f530dd6b31cb226823566509
docker: Error response from daemon: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: exec: "docker-entrypoint.sh": executable file not found in $PATH: unknown.

# docker build --no-cache --tag mongo .
# cd /home/core
# docker run --name mongo -v /home/core/mongo-files/data:/data/db -v /home/core/mongo-files:/opt/keyfile --hostname="node1.example.com" -p 27017:27017 -d mongo  --smallfiles
docker: Error response from daemon: Conflict. The container name "/mongo" is already in use by container "a147ac506a785e8abe1c9e0b2d6abde3d0fa0241f530dd6b31cb226823566509". You have to remove (or rename) that container to be able to reuse that name.
# docker stop mongo
# docker rm mongo

# docker logs 560a43e4f6a24b1188500807464cc4abd8b4397540bb409eca23500f9dc2e9d8
Error parsing command line: unrecognised option '--smallfiles'

# mongo
MongoDB shell version v4.2.24
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("0809e33d-6030-4db9-8754-30716230bb5e") }
MongoDB server version: 4.2.24

# export node1=192.168.56.103
# export node2=192.168.56.104
# export node3=192.168.56.105

# docker logs e15a1bb64cb4aa2aaf47a22ad67f80192c4a80706782237706fea7c4ec9c130c
2023-05-03T19:12:30.855+0000 I  CONTROL  [main] Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'
2023-05-03T19:12:30.857+0000 W  ASIO     [main] No TransportLayer configured during NetworkInterface startup
2023-05-03T19:12:30.857+0000 I  ACCESS   [main] Error reading file /opt/keyfile/mongodb-keyfile: No such file or directory

# chmod -R 777 *
# docker logs 9c84b6100ad0eb84131fbeb62cf8e9a674fd543510d2df4433c0cf39c3573289
2023-05-03T21:43:09.310+0000 I  CONTROL  [main] Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'
2023-05-03T21:43:09.310+0000 W  ASIO     [main] No TransportLayer configured during NetworkInterface startup
2023-05-03T21:43:09.310+0000 I  ACCESS   [main] Error reading file /opt/keyfile/mongodb-keyfile: No such file or directory

# mv mongodb-keyfile mongo-files/
# docker logs ef13fa326db8a2c6f434b2890ab566a8b287830b9a55eb2ee21a882635d695eb
2023-05-03T21:53:00.066+0000 I  CONTROL  [main] Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'
2023-05-03T21:53:00.066+0000 W  ASIO     [main] No TransportLayer configured during NetworkInterface startup
2023-05-03T21:53:00.067+0000 I  ACCESS   [main] permissions on /opt/keyfile/mongodb-keyfile are too open

# chmod 600 mongo-files/mongodb-keyfile
# docker run \
--name mongo \
-v /home/core/mongo-files/data:/data/db \
-v /home/core/mongo-files:/opt/keyfile \
--hostname="node1.example.com" \
--add-host node1.example.com:${node1} \
--add-host node2.example.com:${node2} \
--add-host node3.example.com:${node3} \
-p 27017:27017 -d mongo --keyFile /opt/keyfile/mongodb-keyfile \
--replSet "rs0"
```
* https://github.com/docker-library/postgres/issues/296
  * or you need to manually "chmod +x" that script file before you build.
  * 
* https://stackoverflow.com/questions/35594987/how-to-force-docker-for-a-clean-build-of-an-image
* https://www.ibm.com/docs/en/connect-direct/6.0.0?topic=environment-troubleshooting-in-docker-container


#### scp to node2/3: Perform on Node 1
```
root@cinder:/home/core# scp -rp mongo-files/ vagrant@192.168.56.104:/home/vagrant
root@cinder:/home/core# scp -rp mongo-files/ vagrant@192.168.56.105:/home/vagrant
# docker save -o localmongo.tar mongo
# scp localmongo.tar vagrant@192.168.56.104:/home/vagrant
```
* https://stackoverflow.com/questions/23935141/how-to-copy-docker-images-from-one-host-to-another-without-using-a-repository

#### Perform on Node 2

```
# mkdir -p /home/core
# cd /home/core 
# docker load -i ../vagrant/localmongo.tar 
5f70bf18a086: Loading layer [==================================================>]  1.024kB/1.024kB
8b116ab6d885: Loading layer [==================================================>]  90.17MB/90.17MB
26c7b95fbdda: Loading layer [==================================================>]  337.9kB/337.9kB
4408021c9e9f: Loading layer [==================================================>]  14.92MB/14.92MB
e93e81fc0226: Loading layer [==================================================>]  97.28kB/97.28kB
c73fce4b8c78: Loading layer [==================================================>]  2.146MB/2.146MB
f72e2ba2d4dd: Loading layer [==================================================>]  86.53kB/86.53kB
812bfd78a90e: Loading layer [==================================================>]  289.6MB/289.6MB
8d2e1390b696: Loading layer [==================================================>]  2.048kB/2.048kB
Loaded image: mongo:2.6.5
b7e0fa7bfe7f: Loading layer [==================================================>]  65.52MB/65.52MB
3c417208f103: Loading layer [==================================================>]    405kB/405kB
fb16ef5abed5: Loading layer [==================================================>]   18.1MB/18.1MB
4e44cc5c22ac: Loading layer [==================================================>]  3.547MB/3.547MB
b1cfd9d4b8b5: Loading layer [==================================================>]  2.048kB/2.048kB
059d71c7b256: Loading layer [==================================================>]  5.632kB/5.632kB
f77f2c214b02: Loading layer [==================================================>]  3.584kB/3.584kB
e634f7dd71ce: Loading layer [==================================================>]    305MB/305MB
d113d643ffff: Loading layer [==================================================>]  17.41kB/17.41kB
````

### Docker run the primary and secondary mongodb containers

The following steps are exactly the same as the medium post. However, one thing the medium post didn't point out clearly is that the first "docker run" not just tests the mongodb image but also creates the necessary data and stores these data outside the container: authentication passwords, etc for the subsequent operations.

#### Perform on Node 1
```
root@cinder:/home/core# docker stop mongo
mongo
root@cinder:/home/core# docker rm mongo
mongo
root@cinder:/home/core# rm -rf mongo-files/data/
root@cinder:/home/core# docker run --name mongo \
> -v /home/core/mongo-files/data:/data/db \
> -v /home/core/mongo-files:/opt/keyfile \
> --hostname="node1.example.com" \
> -p 27017:27017 \
> -d mongo
23bb1bca34a9ae8fafa3948e33ad639747638b0745c46d7e9e2d9fc83e4217f5
root@cinder:/home/core# docker exec -it mongo /bin/bash
root@node1:/# mongo
MongoDB shell version v4.2.24
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("4f386ae2-9c60-47bf-9390-1d0d3eb675a7") }
MongoDB server version: 4.2.24
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
	https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
	https://community.mongodb.com
Server has startup warnings: 
2023-05-04T03:37:50.653+0000 I  STORAGE  [initandlisten] 
2023-05-04T03:37:50.653+0000 I  STORAGE  [initandlisten] ** WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
2023-05-04T03:37:50.653+0000 I  STORAGE  [initandlisten] **          See http://dochub.mongodb.org/core/prodnotes-filesystem
2023-05-04T03:37:50.780+0000 I  CONTROL  [initandlisten] 
2023-05-04T03:37:50.780+0000 I  CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2023-05-04T03:37:50.780+0000 I  CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2023-05-04T03:37:50.780+0000 I  CONTROL  [initandlisten] 
---
Enable MongoDB's free cloud-based monitoring service, which will then receive and display
metrics about your deployment (disk utilization, CPU, operation statistics, etc).

The monitoring data will be available on a MongoDB website with a unique URL accessible to you
and anyone you share the URL with. MongoDB may use this information to make product
improvements and to suggest MongoDB products and deployment options to you.

To enable free monitoring, run the following command: db.enableFreeMonitoring()
To permanently disable this reminder, run the following command: db.disableFreeMonitoring()
---

> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
> use admin
switched to db admin
> db.createUser( {
...      user: "siteUserAdmin",
...      pwd: "password",
...      roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
...    });
Successfully added user: {
	"user" : "siteUserAdmin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		}
	]
}
> db.createUser( {
...      user: "siteRootAdmin",
...      pwd: "password",
...      roles: [ { role: "root", db: "admin" } ]
...    });
Successfully added user: {
	"user" : "siteRootAdmin",
	"roles" : [
		{
			"role" : "root",
			"db" : "admin"
		}
	]
}
> exit
bye
root@node1:/# exit
exit
root@cinder:/home/core# docker stop mongo
mongo
root@cinder:/home/core# docker rm mongo
mongo
root@cinder:/home/core# docker run \
> --name mongo \
> -v /home/core/mongo-files/data:/data/db \
> -v /home/core/mongo-files:/opt/keyfile \
> --hostname="node1.example.com" \
> --add-host node1.example.com:${node1} \
> --add-host node2.example.com:${node2} \
> --add-host node3.example.com:${node3} \
> -p 27017:27017 -d mongo --keyFile /opt/keyfile/mongodb-keyfile \
> --replSet "rs0"
62527bdd5ae71906041e7687fa5dd015232ee4b0021dc666a0e08d694880442d
root@cinder:/home/core# docker exec -it mongo /bin/bash
root@node1:/# mongo
MongoDB shell version v4.2.24
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("06871bc1-8643-45b9-90b6-aa423f6f9b7d") }
MongoDB server version: 4.2.24
> use admin
switched to db admin
> db.auth("siteRootAdmin", "password");
1
> rs.initiate()
{
	"info2" : "no configuration specified. Using a default configuration for the set",
	"me" : "node1.example.com:27017",
	"ok" : 1
}
rs0:SECONDARY> 
rs0:PRIMARY> rs.conf()
{
	"_id" : "rs0",
	"version" : 1,
	"protocolVersion" : NumberLong(1),
	"writeConcernMajorityJournalDefault" : true,
	"members" : [
		{
			"_id" : 0,
			"host" : "node1.example.com:27017",
			"arbiterOnly" : false,
			"buildIndexes" : true,
			"hidden" : false,
			"priority" : 1,
			"tags" : {
				
			},
			"slaveDelay" : NumberLong(0),
			"votes" : 1
		}
	],
	"settings" : {
		"chainingAllowed" : true,
		"heartbeatIntervalMillis" : 2000,
		"heartbeatTimeoutSecs" : 10,
		"electionTimeoutMillis" : 10000,
		"catchUpTimeoutMillis" : -1,
		"catchUpTakeoverDelayMillis" : 30000,
		"getLastErrorModes" : {
			
		},
		"getLastErrorDefaults" : {
			"w" : 1,
			"wtimeout" : 0
		},
		"replicaSetId" : ObjectId("64532908d78fc6cecef75e60")
	}
}
```


#### Perform on Node 2
```
# export node1=192.168.56.103
# export node2=192.168.56.104
# export node3=192.168.56.105
# mkdir -p /home/core
# cd /home/core
# # install docker ; same as before 
# docker load -i ../vagrant/localmongo.tar 
5f70bf18a086: Loading layer [==================================================>]  1.024kB/1.024kB
8b116ab6d885: Loading layer [==================================================>]  90.17MB/90.17MB
26c7b95fbdda: Loading layer [==================================================>]  337.9kB/337.9kB
4408021c9e9f: Loading layer [==================================================>]  14.92MB/14.92MB
e93e81fc0226: Loading layer [==================================================>]  97.28kB/97.28kB
c73fce4b8c78: Loading layer [==================================================>]  2.146MB/2.146MB
f72e2ba2d4dd: Loading layer [==================================================>]  86.53kB/86.53kB
812bfd78a90e: Loading layer [==================================================>]  289.6MB/289.6MB
8d2e1390b696: Loading layer [==================================================>]  2.048kB/2.048kB
Loaded image: mongo:2.6.5
b7e0fa7bfe7f: Loading layer [==================================================>]  65.52MB/65.52MB
3c417208f103: Loading layer [==================================================>]    405kB/405kB
fb16ef5abed5: Loading layer [==================================================>]   18.1MB/18.1MB
4e44cc5c22ac: Loading layer [==================================================>]  3.547MB/3.547MB
b1cfd9d4b8b5: Loading layer [==================================================>]  2.048kB/2.048kB
059d71c7b256: Loading layer [==================================================>]  5.632kB/5.632kB
f77f2c214b02: Loading layer [==================================================>]  3.584kB/3.584kB
e634f7dd71ce: Loading layer [==================================================>]    305MB/305MB
d113d643ffff: Loading layer [==================================================>]  17.41kB/17.41kB

# export node1=192.168.56.103
# export node2=192.168.56.104
# export node3=192.168.56.105

# chmod 600 mongo-files/mongodb-keyfile
# chown 999 mongo-files/mongodb-keyfile

docker run \
--name mongo \
-v /home/core/mongo-files/data:/data/db \
-v /home/core/mongo-files:/opt/keyfile \
--hostname="node2.example.com" \
--add-host node1.example.com:${node1} \
--add-host node2.example.com:${node2} \
--add-host node3.example.com:${node3} \
-p 27017:27017 -d mongo --keyFile /opt/keyfile/mongodb-keyfile \
--replSet "rs0"
```


#### Perform on Node 3
```
# export node1=192.168.56.103
# export node2=192.168.56.104
# export node3=192.168.56.105
# mkdir -p /home/core
# cd /home/core
# # install docker ; same as before 
# docker load -i ../vagrant/localmongo.tar

export node1=192.168.56.103
export node2=192.168.56.104
export node3=192.168.56.105

chmod 600 mongo-files/mongodb-keyfile
chown 999 mongo-files/mongodb-keyfile

docker run \
--name mongo \
-v /home/core/mongo-files/data:/data/db \
-v /home/core/mongo-files:/opt/keyfile \
--hostname="node3.example.com" \
--add-host node1.example.com:${node1} \
--add-host node2.example.com:${node2} \
--add-host node3.example.com:${node3} \
-p 27017:27017 -d mongo --keyFile /opt/keyfile/mongodb-keyfile \
--replSet "rs0"

```

#### Perform on Node 1
```
rs0:PRIMARY> rs.add("node2.example.com")
{
	"ok" : 1,
	"$clusterTime" : {
		"clusterTime" : Timestamp(1683172148, 1),
		"signature" : {
			"hash" : BinData(0,"zPivRB9iJ4FFTJ4GmMDA8lnUayc="),
			"keyId" : NumberLong("7229166941196255237")
		}
	},
	"operationTime" : Timestamp(1683172148, 1)
}
rs0:PRIMARY> rs.add("node3.example.com")
{
	"ok" : 1,
	"$clusterTime" : {
		"clusterTime" : Timestamp(1683172157, 1),
		"signature" : {
			"hash" : BinData(0,"WWyRrnV+zwmdB23PN+3ykV3SuG4="),
			"keyId" : NumberLong("7229166941196255237")
		}
	},
	"operationTime" : Timestamp(1683172157, 1)
}
rs0:PRIMARY> rs.status()
{
	"set" : "rs0",
	"date" : ISODate("2023-05-04T03:49:25.517Z"),
	"myState" : 1,
	"term" : NumberLong(1),
	"syncingTo" : "",
	"syncSourceHost" : "",
	"syncSourceId" : -1,
	"heartbeatIntervalMillis" : NumberLong(2000),
	"majorityVoteCount" : 2,
	"writeMajorityCount" : 2,
	"optimes" : {
		"lastCommittedOpTime" : {
			"ts" : Timestamp(1683172157, 1),
			"t" : NumberLong(1)
		},
		"lastCommittedWallTime" : ISODate("2023-05-04T03:49:17.998Z"),
		"readConcernMajorityOpTime" : {
			"ts" : Timestamp(1683172157, 1),
			"t" : NumberLong(1)
		},
		"readConcernMajorityWallTime" : ISODate("2023-05-04T03:49:17.998Z"),
		"appliedOpTime" : {
			"ts" : Timestamp(1683172157, 1),
			"t" : NumberLong(1)
		},
		"durableOpTime" : {
			"ts" : Timestamp(1683172157, 1),
			"t" : NumberLong(1)
		},
		"lastAppliedWallTime" : ISODate("2023-05-04T03:49:17.998Z"),
		"lastDurableWallTime" : ISODate("2023-05-04T03:49:17.998Z")
	},
	"lastStableRecoveryTimestamp" : Timestamp(1683172122, 1),
	"lastStableCheckpointTimestamp" : Timestamp(1683172122, 1),
	"electionCandidateMetrics" : {
		"lastElectionReason" : "electionTimeout",
		"lastElectionDate" : ISODate("2023-05-04T03:39:52.344Z"),
		"electionTerm" : NumberLong(1),
		"lastCommittedOpTimeAtElection" : {
			"ts" : Timestamp(0, 0),
			"t" : NumberLong(-1)
		},
		"lastSeenOpTimeAtElection" : {
			"ts" : Timestamp(1683171592, 1),
			"t" : NumberLong(-1)
		},
		"numVotesNeeded" : 1,
		"priorityAtElection" : 1,
		"electionTimeoutMillis" : NumberLong(10000),
		"newTermStartDate" : ISODate("2023-05-04T03:39:52.358Z"),
		"wMajorityWriteAvailabilityDate" : ISODate("2023-05-04T03:39:52.362Z")
	},
	"members" : [
		{
			"_id" : 0,
			"name" : "node1.example.com:27017",
			"health" : 1,
			"state" : 1,
			"stateStr" : "PRIMARY",
			"uptime" : 595,
			"optime" : {
				"ts" : Timestamp(1683172157, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2023-05-04T03:49:17Z"),
			"syncingTo" : "",
			"syncSourceHost" : "",
			"syncSourceId" : -1,
			"infoMessage" : "",
			"electionTime" : Timestamp(1683171592, 2),
			"electionDate" : ISODate("2023-05-04T03:39:52Z"),
			"configVersion" : 3,
			"self" : true,
			"lastHeartbeatMessage" : ""
		},
		{
			"_id" : 1,
			"name" : "node2.example.com:27017",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
			"uptime" : 16,
			"optime" : {
				"ts" : Timestamp(1683172157, 1),
				"t" : NumberLong(1)
			},
			"optimeDurable" : {
				"ts" : Timestamp(1683172157, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2023-05-04T03:49:17Z"),
			"optimeDurableDate" : ISODate("2023-05-04T03:49:17Z"),
			"lastHeartbeat" : ISODate("2023-05-04T03:49:24.011Z"),
			"lastHeartbeatRecv" : ISODate("2023-05-04T03:49:24.563Z"),
			"pingMs" : NumberLong(0),
			"lastHeartbeatMessage" : "",
			"syncingTo" : "node1.example.com:27017",
			"syncSourceHost" : "node1.example.com:27017",
			"syncSourceId" : 0,
			"infoMessage" : "",
			"configVersion" : 3
		},
		{
			"_id" : 2,
			"name" : "node3.example.com:27017",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
			"uptime" : 7,
			"optime" : {
				"ts" : Timestamp(1683172157, 1),
				"t" : NumberLong(1)
			},
			"optimeDurable" : {
				"ts" : Timestamp(1683172157, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2023-05-04T03:49:17Z"),
			"optimeDurableDate" : ISODate("2023-05-04T03:49:17Z"),
			"lastHeartbeat" : ISODate("2023-05-04T03:49:24.012Z"),
			"lastHeartbeatRecv" : ISODate("2023-05-04T03:49:25.326Z"),
			"pingMs" : NumberLong(0),
			"lastHeartbeatMessage" : "",
			"syncingTo" : "",
			"syncSourceHost" : "",
			"syncSourceId" : -1,
			"infoMessage" : "",
			"configVersion" : 3
		}
	],
	"ok" : 1,
	"$clusterTime" : {
		"clusterTime" : Timestamp(1683172157, 1),
		"signature" : {
			"hash" : BinData(0,"WWyRrnV+zwmdB23PN+3ykV3SuG4="),
			"keyId" : NumberLong("7229166941196255237")
		}
	},
	"operationTime" : Timestamp(1683172157, 1)
}
rs0:PRIMARY>
```

### insert data at the primary mongodb instance and try access at the secondary mongodb instances

#### Perform on Node 1
```
rs0:PRIMARY> db.auth("siteRootAdmin", "password");
Error: Authentication failed.
0
rs0:PRIMARY> use admin
switched to db admin
rs0:PRIMARY> db.auth("siteRootAdmin", "password");
1
rs0:PRIMARY> db.employee.insert({_id:10001,name:'Subhashini'});
WriteResult({ "nInserted" : 1 })
rs0:PRIMARY> db.employee.find()
{ "_id" : 10001, "name" : "Subhashini" }
rs0:PRIMARY>  db.employee.insert({_id:10002,name:'Shobana'});
WriteResult({ "nInserted" : 1 })
rs0:PRIMARY> db.employee.find()
{ "_id" : 10001, "name" : "Subhashini" }
{ "_id" : 10002, "name" : "Shobana" }
```


#### Perform on Node 3
![](https://i.imgur.com/AZFLJHz.png)


```
rs0:SECONDARY> use admin
switched to db admin
rs0:SECONDARY> show dbs
rs0:SECONDARY> db.employee.find()
Error: error: {
	"operationTime" : Timestamp(1683172712, 1),
	"ok" : 0,
	"errmsg" : "command find requires authentication",
	"code" : 13,
	"codeName" : "Unauthorized",
	"$clusterTime" : {
		"clusterTime" : Timestamp(1683172712, 1),
		"signature" : {
			"hash" : BinData(0,"ov8MU8DO2lfIwVciD7v94FTWruI="),
			"keyId" : NumberLong("7229166941196255237")
		}
	}
}
rs0:SECONDARY> db.auth("siteRootAdmin", "password");
1
rs0:SECONDARY> db.employee.find()
Error: error: {
	"operationTime" : Timestamp(1683172770, 2),
	"ok" : 0,
	"errmsg" : "not master and slaveOk=false",
	"code" : 13435,
	"codeName" : "NotPrimaryNoSecondaryOk",
	"$clusterTime" : {
		"clusterTime" : Timestamp(1683172770, 2),
		"signature" : {
			"hash" : BinData(0,"38ApWwSiJC4N7xrfaphHamdQl8I="),
			"keyId" : NumberLong("7229166941196255237")
		}
	}
}
rs0:SECONDARY> rs.slaveOk()
WARNING: slaveOk() is deprecated and may be removed in the next major release. Please use secondaryOk() instead.
rs0:SECONDARY> db.employee.find()
{ "_id" : 10001, "name" : "Subhashini" }
{ "_id" : 10002, "name" : "Shobana" }
```

#### Perform on Node 2
![](https://i.imgur.com/ggoQB8m.png)

```
root@swift1:~# cd /home/core/
root@swift1:/home/core# docker stop mongo
mongo
root@swift1:/home/core# docker rm mongo
mongo
root@swift1:/home/core# export node1=192.168.56.103
root@swift1:/home/core# export node2=192.168.56.104
root@swift1:/home/core# export node3=192.168.56.105
root@swift1:/home/core# rm mongo-files/data/ -rf
root@swift1:/home/core# ls mongo-files/mongodb-keyfile 
mongo-files/mongodb-keyfile
root@swift1:/home/core# docker run \
> --name mongo \
> -v /home/core/mongo-files/data:/data/db \
> -v /home/core/mongo-files:/opt/keyfile \
> --hostname="node2.example.com" \
> --add-host node1.example.com:${node1} \
> --add-host node2.example.com:${node2} \
> --add-host node3.example.com:${node3} \
> -p 27017:27017 -d mongo --keyFile /opt/keyfile/mongodb-keyfile \
> --replSet "rs0"
003fa2f53e3edb126313a673df723c7665ad72d9f11732e4545026e4e6e522b7
root@swift1:/home/core# docker exec -it mongo /bin/bash
root@node2:/# exit
exit
root@swift1:/home/core# docker exec -it mongo /bin/bash
root@node2:/# mongo
MongoDB shell version v4.2.24
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("5e9c82cc-338e-4548-b0cb-49a4a050c0a9") }
MongoDB server version: 4.2.24
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
	https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
	https://community.mongodb.com
rs0:SECONDARY> use admin
switched to db admin
rs0:SECONDARY> db.auth("siteRootAdmin", "password");
1
rs0:SECONDARY> rs.secondaryOk()
rs0:SECONDARY> db.employee.find()
{ "_id" : 10001, "name" : "Subhashini" }
{ "_id" : 10002, "name" : "Shobana" }
```

### Appendix

#### Dockerfile
```
#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM ubuntu:bionic

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN set -eux; \
	groupadd --gid 999 --system mongodb; \
	useradd --uid 999 --system --gid mongodb --home-dir /data/db mongodb; \
	mkdir -p /data/db /data/configdb; \
	chown -R mongodb:mongodb /data/db /data/configdb

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		ca-certificates \
		gnupg \
		jq \
		numactl \
		procps \
	; \
	rm -rf /var/lib/apt/lists/*

# grab gosu for easy step-down from root (https://github.com/tianon/gosu/releases)
ENV GOSU_VERSION 1.16
# grab "js-yaml" for parsing mongod's YAML config files (https://github.com/nodeca/js-yaml/releases)
ENV JSYAML_VERSION 3.13.1

RUN set -ex; \
	\
	savedAptMark="$(apt-mark showmanual)"; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		wget \
	; \
	rm -rf /var/lib/apt/lists/*; \
	\
	dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')"; \
	wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch"; \
	wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc"; \
	export GNUPGHOME="$(mktemp -d)"; \
	gpg --batch --keyserver hkps://keys.openpgp.org --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4; \
	gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu; \
	gpgconf --kill all; \
	rm -rf "$GNUPGHOME" /usr/local/bin/gosu.asc; \
	\
	wget -O /js-yaml.js "https://github.com/nodeca/js-yaml/raw/${JSYAML_VERSION}/dist/js-yaml.js"; \
# TODO some sort of download verification here
	\
	apt-mark auto '.*' > /dev/null; \
	apt-mark manual $savedAptMark > /dev/null; \
	apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
	\
# smoke test
	chmod +x /usr/local/bin/gosu; \
	gosu --version; \
	gosu nobody true

RUN mkdir /docker-entrypoint-initdb.d

RUN set -ex; \
	export GNUPGHOME="$(mktemp -d)"; \
	set -- 'E162F504A20CDF15827F718D4B7C549A058F8B6B'; \
	for key; do \
		gpg --batch --keyserver keyserver.ubuntu.com --recv-keys "$key"; \
	done; \
	mkdir -p /etc/apt/keyrings; \
	gpg --batch --export "$@" > /etc/apt/keyrings/mongodb.gpg; \
	gpgconf --kill all; \
	rm -rf "$GNUPGHOME"

# Allow build-time overrides (eg. to build image with MongoDB Enterprise version)
# Options for MONGO_PACKAGE: mongodb-org OR mongodb-enterprise
# Options for MONGO_REPO: repo.mongodb.org OR repo.mongodb.com
# Example: docker build --build-arg MONGO_PACKAGE=mongodb-enterprise --build-arg MONGO_REPO=repo.mongodb.com .
ARG MONGO_PACKAGE=mongodb-org
ARG MONGO_REPO=repo.mongodb.org
ENV MONGO_PACKAGE=${MONGO_PACKAGE} MONGO_REPO=${MONGO_REPO}

ENV MONGO_MAJOR 4.2
RUN echo "deb [ signed-by=/etc/apt/keyrings/mongodb.gpg ] http://$MONGO_REPO/apt/ubuntu bionic/${MONGO_PACKAGE%-unstable}/$MONGO_MAJOR multiverse" | tee "/etc/apt/sources.list.d/${MONGO_PACKAGE%-unstable}.list"

# https://docs.mongodb.org/master/release-notes/4.2/
ENV MONGO_VERSION 4.2.24
# 02/23/2023, https://github.com/mongodb/mongo/tree/5e4ec1d24431fcdd28b579a024c5c801b8cde4e2

RUN set -x \
# installing "mongodb-enterprise" pulls in "tzdata" which prompts for input
	&& export DEBIAN_FRONTEND=noninteractive \
	&& apt-get update \
	&& apt-get install -y \
		${MONGO_PACKAGE}=$MONGO_VERSION \
		${MONGO_PACKAGE}-server=$MONGO_VERSION \
		${MONGO_PACKAGE}-shell=$MONGO_VERSION \
		${MONGO_PACKAGE}-mongos=$MONGO_VERSION \
		${MONGO_PACKAGE}-tools=$MONGO_VERSION \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /var/lib/mongodb \
	&& mv /etc/mongod.conf /etc/mongod.conf.orig

VOLUME /data/db /data/configdb

# ensure that if running as custom user that "mongosh" has a valid "HOME"
# https://github.com/docker-library/mongo/issues/524
ENV HOME /data/db

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 27017
CMD ["mongod"]
```
* https://github.com/docker-library/mongo/blob/685ebea/4.2/Dockerfile

#### Vagrantfile
```
# -*- mode: ruby -*-
# vi: set ft=ruby :

require_relative 'config' rescue LoadError

Vagrant.configure("2") do |config|

  OS = "bento/ubuntu-20.04"

  def configVMCapacity(vb, cpus, memory)
    vb.gui = false
    vb.memory = memory
    vb.cpus = cpus
  end

  def setVMForwardedPort(df, name, ports)
    if ports
      ports.each do |port|
        df.vm.network :forwarded_port, guest: port[:NODE_PORT], host: port[:TARGET_PORT], host_ip: "0.0.0.0", id: "#{name}:#{port[:NODE_PORT]}", auto_correct: true
      end
    end
  end

  config.vm.provider "virtualbox"
  config.vm.box = "#{OS}"

  VMS.each do |vm|
    config.vm.define "develop-#{vm[:NAME]}" do |df|
      df.vm.hostname = "#{vm[:NAME]}"
      df.vm.network :private_network, ip: vm[:IP],  auto_config: true
      setVMForwardedPort(df, vm[:NAME], vm[:PORT])
      df.vm.network "public_network", auto_config: false
      df.vm.provider :virtualbox do |vb, override|
        configVMCapacity(vb, vm[:CPUS], vm[:MEMORY_MB])
        file_to_disk = "extra-#{vm[:NAME]}.vdi"
        #puts file_to_disk
        unless File.exist?(file_to_disk)
          vb.customize ['createhd',
                      '--filename', "extra-#{vm[:NAME]}",
                      '--format', 'VDI',
                      '--size', 50000]
        end
	    
        vb.customize ['storageattach', :id,
                    '--storagectl', 'SATA Controller',
                    '--port', 2,
                    '--device', 0,
                    '--type', 'hdd',
                    '--medium', "extra-#{vm[:NAME]}.vdi"]

        file_to_disk = "extra1-#{vm[:NAME]}.vdi"
        unless File.exist?(file_to_disk)
          vb.customize ['createhd',
                      '--filename', "extra1-#{vm[:NAME]}",
                      '--format', 'VDI',
                      '--size', 50000]
        end
	    
        vb.customize ['storageattach', :id,
                    '--storagectl', 'SATA Controller',
                    '--port', 3,
                    '--device', 0,
                    '--type', 'hdd',
                    '--medium', "extra1-#{vm[:NAME]}.vdi"]
        vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
        vb.customize ["modifyvm", :id, "--uartmode1", "file", File::NULL]
      end
    end
  end
end
```

#### config.rb
```
VMS = [
    {
      :NAME => "cinder",
      :IP => "192.168.56.103",
      :MEMORY_MB => 6144,
      :CPUS => 2,
      :PORT => [
        {
          :NODE_PORT => 5000,
          :TARGET_PORT => 30004,
        }
      ]
    },
    {
      :NAME => "swift1",
      :IP => "192.168.56.104",
      :MEMORY_MB => 6144,
      :CPUS => 2,
      :PORT => [
        {
          :NODE_PORT => 30001,
          :TARGET_PORT => 30005,
        }
      ]
    },
    {
      :NAME => "swift2",
      :IP => "192.168.56.105",
      :MEMORY_MB => 6144,
      :CPUS => 2,
      :PORT => [
        {
          :NODE_PORT => 30001,
          :TARGET_PORT => 30006,
        }
      ]
    }
  ]
```
