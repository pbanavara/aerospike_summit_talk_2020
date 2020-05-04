<h2>
  Running Aerospike hybrid configuration in a Docker container
</h2>

These are steps to be followed on a EC2 Ubuntu VM

* First create a new volume on EC2 following [these steps](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html)
* Create the following config file
  

```
    service {
        paxos-single-replica-limit 1 # Number of nodes where the replica count is automatically reduced to 1.
        proto-fd-max 15000
    }

    logging {
        file /var/log/aerospike/aerospike.log {
                context any info
        }
        console {
            context any info
        }
    }

    network {
        service {
                address any
                port 3000
        }

        heartbeat {
                mode multicast
                multicast-group 239.1.99.222
                port 9918

                # To use unicast-mesh heartbeats, remove the 3 lines above, and see
                # aerospike_mesh.conf for alternative.

                interval 150
                timeout 10
        }

        fabric {
                port 3001
        }

        info {
                port 3003
        }
    }

    namespace test {
        replication-factor 2
        memory-size 1G
        storage-engine device {
                device /dev/xvdf
                write-block-size 128k
        }

    }

    namespace bar {
        replication-factor 2
        memory-size 1G
        storage-engine memory
    }
```

* Run the following Docker command
```
sudo docker run -tid --name aerospike -p 3000:3000 -p 3001:3001 -p 3002:3002 -p 3003:3003 -v /opt:/opt/aerospike/etc --device '/dev/xvdf:/dev/xvdf' aerospike/aerospike-server:latest asd --config-file /opt/aerospike/etc/aerospike.conf
```
By using this command the host device /dev/xvdf ( The new volume created) is mapped to the same destination.
Configuration file is assumed to be in /opt directory which is mapped to /opt/aerospike/etc in the container