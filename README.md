
# ***Integration of JENKINS, GITHUB and DOCKER*** 

# Project Description:
- This is a simple CI/CD model for integration **Docker** and **Github** branches using **Jenkins**.
- In short whenever the developer updates website and uplods the code in his github developer branch, Jenkins then automatically downloads the code and deploys it in the system using docker container in developer-docker environment. 
- Quality Management Team(QA) will manually checks the site if it is working fine or not, if yes then they manually trigger the next job in jenkins which will merge the developers updated code with the master branch. 
- As soon as the master branch is commited with the new code it triggers the next job  in Jenkins which will update the Website in the Server.
Note that: If there are any merge conflicts, then it has to be manually updated.

# **REQUIRED SETUP**
 * install linux OS(espcially redhat) 
 * install docker in linux.To install [click here](https://docs.docker.com/engine/install/)
 * install jenkins in linux.Information regarding install [click here](https://www.jenkins.io/download/)
 * install git in linux.To install [click here](https://git-scm.com/download/linux)
 
 
# **Initially the website will be running**
Container                  |  Site
:-------------------------:|:-------------------------:
![](images/ic.png)  |  ![](images/io.png)

# **JENKINS**

### Job1 : As soon as developer pushes the new code to the developer branch Jenkins will fetch the code from github and deploy on docker-developer environment
![](images/j11.png)
![](images/j12.png)
![](images/j13.png)
![](images/j14.png)

### Execute Shell Code:

     sudo cp -v * /root/developer/
     if  sudo docker ps|grep mlopsdev
     then
       exit 0
     else
       sudo docker run -dit -p 6996:80 -v /root/developer/:/usr/local/apache2/htdocs/ --name mlopsdev httpd:latest
     fi

### Below shown is the launched container
![](images/rc.png)

### Job2 : Whenever developer pushes to the master branch, then Jenkins will fetch from master and deploy it on docker master-docker environment.
### (both developer-docker and master-docker environments are different containers)

![](images/j21.png)
![](images/j22.png)
![](images/j23.png)
![](images/j24.png)

### Execute Shell Code:

    sudo cp -v * /root/master/
    if  sudo docker ps|grep mlopsmaster
    then
      exit 0
    else
      sudo docker run -dit -p 9669:80 -v /root/master/:/usr/local/apache2/htdocs/ --name mlopsmaster httpd:latest
    fi




### Job3 : Quality Assessment Team will manually test the website running in developer-docker environment. If it is running fine, they will trigger Jenkins next job which will merge the developer branch to master branch.

![](images/j31.png)
![](images/j32.png)
![](images/j33.png)
![](images/j34.png)
![](images/j35.png)

### Once after the new code is updated at the Master branch the website also gets updated.
### The updated website is shown below

![](images/ro.png)

---

## In collobration with : @madannaik
