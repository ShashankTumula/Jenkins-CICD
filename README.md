# Jenkins-CICD
Automating the delivery of a nodejs app using jenkins and docker

Create AWS EC2 instance
Connect using ssh or ec2 instance connect

Now, run

sudo apt update

    3  sudo apt install openjdk-11-jre
    4  java -version
    5  curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
    6  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
    7  sudo apt-get update 
    8  sudo apt-get install jenkins
    9  sudo systemctl enable jenkins
    10  sudo systemctl start jenkins
    11  sudo systemctl status jenkins

   Use the password to create an admin jenkins account
    12  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    13  history


   ![Screenshot (449)](https://github.com/ShashankTumula/Jenkins-CICD/assets/103590482/9b8f3c00-f3f0-469c-9dcc-a41a30e092cc)
   

   # Create a job in jenkins and build 
   

   ![Screenshot (454)](https://github.com/ShashankTumula/Jenkins-CICD/assets/103590482/52a0f3e5-217c-4a60-b749-fb4ddc80148a)

sudo apt install docker.io,

generate an ssh key using ssh-keygen,

In github add the public key,

In jenkins add the public and private key,

Now start the build, this time app will run in a docker container,

![Screenshot (455)](https://github.com/ShashankTumula/Jenkins-CICD/assets/103590482/f222a09b-a454-4561-8079-27e6d616b631)



Go to the directory provided by jenkins after initial build



create a docker file and enter the following-

FROM node:12.12.0-alpine

WORKDIR app

COPY . .

RUN npm install

EXPOSE 8000

CMD ["node","app.js"]

---------------------------------
docker build . -t node-app

sudo usermod -a -G docker $USER

docker run -d --name node-todo-app -p 8000:8000 todo-node-app


# Got to jenkins job

Execute shell-

docker build . -t node-app-todo

docker run -d --name node-app-container -p 8000:8000 node-app-todo


Now, enable webhooks for the repository and link it to jenkins

# Done!

![Screenshot (462)](https://github.com/ShashankTumula/Jenkins-CICD/assets/103590482/01f50c1f-c93c-4c36-951d-91770d3e919a)

![Screenshot (463)](https://github.com/ShashankTumula/Jenkins-CICD/assets/103590482/6ed03708-f0f4-4013-b3ff-8dd38fdb0768)

# Now, each time you commit some changes, webhook will be triggered which will lead to the next build in Jenkins
