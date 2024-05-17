# A)



´´´
# Create network
# Apparently Docker uses the following ranges by default:
# 172.17.0.0/16", 172.18.0.0/16", "172.19.0.0/16", "172.20.0.0/14", "172.24.0.0/14" "172.28.0.0/14", "192.168.0.0/16".
docker network create tbz
docker network ls
docker inspect tbz


docker run --name busybox1 -d busybox
docker run --name busybox2 -d busybox
docker run --name busybox3 -d --network tbz busybox
docker run --name busybox4 -d --network tbz busybox



# Check IP's
docker inspect
´´´

![alt text](image-1.png)
![alt text](image.png)

