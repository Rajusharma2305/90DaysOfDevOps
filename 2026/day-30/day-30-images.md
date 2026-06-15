# Day 30 – Docker Images & Container Lifecycle

## Objective

Today's goal is to understand:

* Docker Images
* Image Layers
* Container Lifecycle
* Working with Running Containers
* Docker Cleanup Commands

---

# Task 1: Docker Images

## 1. Pull Images from Docker Hub

Pull the following images:

```bash
docker pull nginx
docker pull ubuntu
docker pull alpine
```

### Verify Images

```bash
docker images
```

### Questions to Answer

1. What images are available on your machine?
2. What are their sizes?
3. Which image is smallest?

---

## 2. Compare Ubuntu vs Alpine

Check image sizes:

```bash
docker images
```

### Write Notes

* Why is Alpine much smaller?
* What trade-offs come with a smaller image?

---

## 3. Inspect an Image

Inspect the Nginx image:

```bash
docker image inspect nginx
```

### Find

* Image ID
* Architecture
* OS
* Creation Date
* Environment Variables

---

## 4. Remove an Image

Remove Alpine:

```bash
docker rmi alpine
```

Verify:

```bash
docker images
```

---

# Task 2: Docker Image Layers

## View Image History

```bash
docker image history nginx
```

Observe:

* Multiple layers
* Layer sizes
* Some layers showing 0B

### Write Notes

Answer:

1. What is an image layer?
2. Why does Docker use layers?
3. What benefits do layers provide?
4. Why do some layers show 0B?

---

# Task 3: Container Lifecycle

Create a container without starting it:

```bash
docker create --name lifecycle-demo ubuntu
```

Check status:

```bash
docker ps -a
```

---

## Start Container

```bash
docker start lifecycle-demo
```

Check:

```bash
docker ps -a
```

---

## Pause Container

```bash
docker pause lifecycle-demo
```

Check:

```bash
docker ps -a
```

---

## Unpause Container

```bash
docker unpause lifecycle-demo
```

Check:

```bash
docker ps -a
```

---

## Stop Container

```bash
docker stop lifecycle-demo
```

Check:

```bash
docker ps -a
```

---

## Restart Container

```bash
docker restart lifecycle-demo
```

Check:

```bash
docker ps -a
```

---

## Kill Container

```bash
docker kill lifecycle-demo
```

Check:

```bash
docker ps -a
```

---

## Remove Container

```bash
docker rm lifecycle-demo
```

Verify:

```bash
docker ps -a
```

---

# Task 4: Working with Running Containers

## Run Nginx Container

```bash
docker run -d --name my-nginx -p 8080:80 nginx
```

Verify:

```bash
docker ps
```

---

## View Logs

```bash
docker logs my-nginx
```

---

## Follow Logs in Real Time

```bash
docker logs -f my-nginx
```

Stop following:

```bash
CTRL + C
```

---

## Enter Running Container

```bash
docker exec -it my-nginx bash
```

Explore:

```bash
pwd
ls
cd /usr/share/nginx/html
ls
```

Exit:

```bash
exit
```

---

## Run Command Without Entering Container

```bash
docker exec my-nginx hostname
```

Try:

```bash
docker exec my-nginx ls /
```

---

## Inspect Container

```bash
docker inspect my-nginx
```

Find:

* Container ID
* IP Address
* Port Mapping
* Mounts
* Network Information

---

# Task 5: Cleanup

## Stop All Running Containers

```bash
docker stop $(docker ps -q)
```

---

## Remove All Stopped Containers

```bash
docker container prune
```

OR

```bash
docker rm $(docker ps -aq)
```

---

## Remove Unused Images

```bash
docker image prune
```

Remove everything unused:

```bash
docker system prune -a
```

---

## Check Docker Disk Usage

```bash
docker system df
```

### Observe

* Images Size
* Containers Size
* Local Volumes
* Build Cache
