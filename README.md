# DevOps with Docker - Part 2

## Excercises

## NOTE: Removed db passwords from all docker-compose.yml files, so you'll need to specify your own where needed.
Applies to ex28, ex29, ex210

## Exercise 2.1
[Up](#excercises)

### docker-compose.yml and logs.txt in folder [ex21](ex21)
```
syyspe@debian95:/mnt/devt/DevOps/part2/ex21$ touch logs.txt  
syyspe@debian95:/mnt/devt/DevOps/part2/ex21$  
syyspe@debian95:/mnt/devt/DevOps/part2/ex21$ docker-compose up  
Pulling logger (devopsdockeruh/first_volume_exercise:)...  
latest: Pulling from devopsdockeruh/first_volume_exercise  
741437d97401: Pull complete  
34d8874714d7: Pull complete  
0a108aa26679: Pull complete  
7f0334c36886: Pull complete  
65c95cb8b3be: Pull complete  
a36b708560f8: Pull complete  
4090f912e6c7: Pull complete  
ce5fe2607c2e: Pull complete  
9400f5f657d6: Pull complete  
3ccbeb634bca: Pull complete  
Digest: sha256:0fe91ae116a340214cf013541bd311da7196d34a468e9daf74a8d0fdd3419c78  
Status: Downloaded newer image for devopsdockeruh/first_volume_exercise:latest  
Creating ex21 ... done  
Attaching to ex21  
ex21      | (node:1) ExperimentalWarning: The fs.promises API is experimental  
ex21      | Wrote to file /usr/app/logs.txt  
ex21      | Wrote to file /usr/app/logs.txt  
ex21      | Wrote to file /usr/app/logs.txt  
ex21      | Wrote to file /usr/app/logs.txt  
^CGracefully stopping... (press Ctrl+C again to force)  
Killing ex21  ... done  
syyspe@debian95:/mnt/devt/DevOps/part2/ex21$  
```

## Excercise 2.2
[Up](#excercises)

### docker-compose.yml in folder [ex22](ex22)
### Message: Ports configured correctly!!

```
syyspe@debian95:/mnt/devt/DevOps/part2/ex22$ docker-compose up  
Creating network "ex22_default" with the default driver  
Creating ex22 ... done  
Attaching to ex22  
ex22      |  
ex22      | > ports_exercise@1.0.0 start /usr/app  
ex22      | > node index.js  
ex22      |  
ex22      | Listening on port 80, this means inside of the container. Use -p to map the port to a port of your local machine.  
^CGracefully stopping... (press Ctrl+C again to force)  
Stopping ex22 ...  
Killing ex22  ... done  
syyspe@debian95:/mnt/devt/DevOps/part2/ex22$  
```

## Excercise 2.3
[Up](#excercises)

### Dockerfiles in folder [ex23](ex23)

I had already deleted the backend and frontend images and code from part 1, so what I did was I created directories  
backend and frontend, copied respective dockerfiles to those directories from part 1, pulled the code again from git,  
and built/launched using the following docker-compose.yml and ```docker-compose up``` command:  

```
version: '3'

services:
  backend:
    build:
      context: ./backend
    container_name: ex23_back
    ports:
      - 8000:8000
  frontend:
    build:
      context: ./frontend
    container_name: ex23_front
    ports:
      - 5000:5000
    depends_on: 
      - backend
```

That worked OK and the application functioned as expected. Once I had the images recreated, the following  
docker-compose.yml worked as well:  

```
version: '3'

services:
  backend:
    image: ex23_backend
    container_name: ex23_back
    ports:
      - 8000:8000
  frontend:
    image: ex23_frontend
    container_name: ex23_front
    ports:
      - 5000:5000
    depends_on: 
      - backend
```

## Excercise 2.4
[Up](#excercises)

Passing this one, as I'm running docker on virtual machine, the localhost approach doesn't work  
(The service is not available via localhost, but via the virtual machine IP address). I could maybe   
have used curl etc to test from vm.

## Excercise 2.5
[Up](#excercises)

### Dockerfile in folder [ex25](ex25)

Working! It took 0.195 seconds.  

ex25_back   | Got from redis pong

## Excercise 2.6
[Up](#excercises)

### Dockerfile in folder [ex26](ex26)

## Excercise 2.7
[Up](#excercises)

### Dockerfile in folder [ex27](ex27)

Required defining Python interpreter with shebang in backend/app.py,  
otherwise crashed on subprocess creation after model became available.   
This on debian stretch image running on vmware.  

I created local folders for the volumes so that it was easier to follow progress.  

## Excercise 2.8
[Up](#excercises)

### Dockerfile in folder [ex28](ex28)
### NOTE: define db password!

Exercise 2.8 button: Working! 

## Excercise 2.9
[Up](#excercises)

### Dockerfile in folder [ex29](ex29)
### NOTE: define db password!

Removed nginx so that the message buttons worked. Database persists in dir under my home dir.  

## Excercise 2.10
[Up](#excercises)

### Dockerfiles in folders [ex210](ex210) [ex210/backend](ex210/backend) [ex210/frontend](ex210/frontend)
### NOTE: define db password!

Added nginx back to config, edited backend/frontend Dockerfiles to exclude port definitions from  
backend/frontend URLs, and rebuilt backend/frontend images. 

[Image](#ex210/browser-ex210.png) to prove it is working.





