#### Please follow these instructions for setting up Aerospike on Docker

* Should you want to build Aerospike in an in-memory mode just use this Docker command:
  
```
docker run -d -v <source_dir>:<dest_dir> --name <container_name> -p 3000:3000 -p 3001:3001 -p 3002:3002 -p 3003:3003 aerospike/aerospike-server asd --foreground --config-file <dest_dir>/aerospike.conf
```
Where
* source_dir is the directory containing the configuration file
* dest_dir is the mapping of source directory to a destination inside the container. Please ensure this is not the same as source directory.

If Docker starts successfully you should see something like this

```
CONTAINER ID        IMAGE                               COMMAND                  CREATED             STATUS              PORTS                                   NAMES
c268fbd7e0bb        aerospike/aerospike-server:latest   "/entrypoint.sh asd …"   2 weeks ago         Up 2 seconds        0.0.0.0:3000->3000/tcp, 3001-3003/tcp   python_web_app_aerospike_1
```

* To start Aerospike in a hybrid mode, data stored on disk and index in memory use [Hybrid link](docker_aerospike_hybrid/README.md)
* To build a Dockerfile from scratch for a simple web application that uses Aerospike use [Python web app](python_web_app/README.md)
