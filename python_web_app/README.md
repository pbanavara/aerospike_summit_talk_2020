#### A few instructions for building and composing the docker image

* This configuration file is more or less a guide.
* I am highlighting some additional steps needed to get the image working
* This is for a specific Aerospike configuration - data in memory backed up on disk
  
Once you have created the python sources create the Dockerfile and the docker-compose.yml files.

* Run
` docker-compose build
`

* Once the images are built, run
  `docker-compose up -d`

Neither of the containers will start as evidenced in `docker ps`

* List the containers using `docker ps -a`
* Login to the aerospike container using `docker exec -it container-id /bin/bash`
* Check the logs at the configured location /etc/aerospike/aerospike.log (This is set in the config file)
* If the data file is missing at the said location, create the data file and directory
Exit the shell

* Again run `docker-compose up -d`
* Now the aerospike container will start but not the Python container
* Again run `docker-compose up -d` to start the Python app container

##### Working with the web app

* The app exposes a POST and GET interface to add and view records
* After the container is running POST some data