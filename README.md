# Jenkins-CICD
Automating the delivery of a nodejs app using jenkins and docker

Create AWS EC2 instance
Connect using ssh or ec2 instance connect

Now, run the following in ubuntu(i used ec2)

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

# OUTPUT-
Started by user Shashank Patel
Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/demo-app
The recommended git tool is: NONE
using credential github-jenkins-demo
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/demo-app/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/ShashankTumula/nodejs-todo.git # timeout=10
Fetching upstream changes from https://github.com/ShashankTumula/nodejs-todo.git
 > git --version # timeout=10
 > git --version # 'git version 2.34.1'
using GIT_SSH to set credentials genkins github integration
Verifying host key using known hosts file
You're using 'Known hosts file' strategy to verify ssh host keys, but your known_hosts file does not exist, please go to 'Manage Jenkins' -> 'Security' -> 'Git Host Key Verification Configuration' and configure host key verification.
 > git fetch --tags --force --progress -- https://github.com/ShashankTumula/nodejs-todo.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision a38e66e0ab0e3aeba406c9300e209aee249e275f (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f a38e66e0ab0e3aeba406c9300e209aee249e275f # timeout=10
Commit message: "Merge pull request #187 from LondheShubham153/LondheShubham153-patch-22"
 > git rev-list --no-walk a38e66e0ab0e3aeba406c9300e209aee249e275f # timeout=10
[demo-app] $ /bin/sh -xe /tmp/jenkins11698672096673721826.sh
+ docker build . -t todo-node-app
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  25.34MB

Step 1/7 : FROM node:12.2.0-alpine
 ---> f391dabf9dce
Step 2/7 : WORKDIR app
 ---> Using cache
 ---> 64f96360b3f4
Step 3/7 : COPY . .
 ---> Using cache
 ---> 8c88f1c9bb10
Step 4/7 : RUN npm install
 ---> Using cache
 ---> 031b64e67fad
Step 5/7 : RUN npm run test
 ---> Using cache
 ---> e827e607f18f
Step 6/7 : EXPOSE 8000
 ---> Using cache
 ---> 2bbcc0c1633f
Step 7/7 : CMD ["node","app.js"]
 ---> Using cache
 ---> 0bb1f80a6cd6
Successfully built 0bb1f80a6cd6
Successfully tagged todo-node-app:latest
+ docker run -d --name node-todo-app -p 8000:8000 todo-node-app
e68c2c682e7e61a76ebd2c9c6f7ecc48a25c0442b0948225e0210f4d9db5fc11
Finished: SUCCESS

# Done!

![Screenshot (462)](https://github.com/ShashankTumula/Jenkins-CICD/assets/103590482/01f50c1f-c93c-4c36-951d-91770d3e919a)

![Screenshot (463)](https://github.com/ShashankTumula/Jenkins-CICD/assets/103590482/6ed03708-f0f4-4013-b3ff-8dd38fdb0768)

# Now, each time you commit some changes, webhook will be triggered which will lead to the next build in Jenkins
