# Docker Workshop: Getting Started

This repository is a personal fork of the **Docker Getting Started App**, serving as a hands-on lab environment for completing the official Docker Workshop. It documents the deployment of containerized applications within a cloud-native infrastructure.

---

##  Reference Material
* **Official Workshop Guide:** [Docker Workshop Documentation](https://docs.docker.com/get-started/)
* **Original Repository:** [docker/getting-started](https://github.com/docker/getting-started)

##  Prerequisites & Environment
* **Cloud Provider:** Google Cloud Platform (GCP) via the Student Credit program.
* **Host OS:** Dedicated Compute Engine VM running **Ubuntu 22.04 LTS**.
* **Hardware Instance:** `e2-medium` (or your specific machine type).

##  Deployment Steps

### 1. VM Provisioning
* Configured a Google Compute Engine (GCE) instance named `vmubuntu`.
* **Access Control:** Established secure remote management via **SSH**.
* **Documentation:** For specific firewall rules and instance settings, refer to my https://github.com/diovsset/getting-started-app/blob/main/setup.md

### 2. Docker Installation
* Installed Docker
  Now, we are in the VM install Docker from https://docs.docker.com/engine/install/ubuntu/.
  - [ ] As per notes: Please install using the "install using apt" on your virtual machine.
  - [ ]  sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  - [ ]  sudo usermod -aG docker `whoami`
  - [ ]  Then logout/login
* Verified installation using `docker --version` and `docker compose version`.

### 3. Progress Tracking
I am documenting my journey through the workshop modules below, specifically focusing on multi-container orchestration and persistent cloud deployments.
### 📦 Part 1: Containerize an Application
* **Action:** Created a `Dockerfile` to package the environment and dependencies.
* **Key Learning:** Understood the difference between an **Image** (the blueprint) and a **Container** (the running instance).
* **Command:** `docker build -t getting-started .`
  
  1. Fork the repository rather than cloning, as this avoids the need to push back from the server
     <img width="902" height="208" alt="unknown" src="https://github.com/user-attachments/assets/ffcf4ee6-cc6a-456c-b660-dd579f9cd3b7" />
  2. After forking the repository, clone it inside the VM.
  <img width="1600" height="428" alt="unknown" src="https://github.com/user-attachments/assets/8c14b9de-f2a6-4f58-a402-7e7d1337f8a4" />
  
  <img width="1600" height="216" alt="unknown" src="https://github.com/user-attachments/assets/ae50e17a-b283-4691-b27f-ee90c4049bab" />
  
  Verify the cloned repository by navigating into the directory and listing its contents:
      cd getting-started
      ls -a
      
  <img width="1600" height="847" alt="unknown" src="https://github.com/user-attachments/assets/b19c8a23-575c-45a0-93d0-83ce0546b575" />

> [!NOTE]
> The forked repository already contained a Dockerfile. To follow the workshop from scratch, I cleared the existing file using nano Dockerfile and replaced the content with the official workshop instructions."

  <img width="1600" height="1321" alt="unknown" src="https://github.com/user-attachments/assets/ad0e3c22-ed67-45b7-8092-0aea08b907c1" />

  3. Clear the existing Dockerfile and paste the following content inside (see Docker Workshop Build the App Image step 1)
     
  <img width="1600" height="785" alt="unknown" src="https://github.com/user-attachments/assets/98f2931e-d141-4134-86ac-fa32b366633a" />

  Saving and Exiting (Nano Editor)
  If you are using the nano editor on your VM, follow these steps to save your changes:
    - Save: Press Control + O (Write Out).
    - Confirm: Press Enter to keep the filename as Dockerfile.
    - Exit: Press Control + X to return to the command line.
     
  4. Build the Image. Once the file is saved, use the following command to build your Docker image:
     ```bash docker build -t getting-started .```
     
  Result:
  
  <img width="1600" height="1269" alt="unknown" src="https://github.com/user-attachments/assets/edcc4487-5bc2-401e-81a9-f624b5ad6ffb" />  
  
  5. Run your container using the docker run command and specify the name of the image you just created:
     ```bash docker run -d -p 8080:3000 getting-started```
<img width="1600" height="129" alt="Loud-adminivaabuntu-getting-started-appdocker run -d p 80803000 getting-started" src="https://github.com/user-attachments/assets/18a799ef-804e-4342-942a-92416b0c326c" />
     
  7. Visit the app on http://<extip>
  <img width="778" height="464" alt="Not Secure - 34840 199" src="https://github.com/user-attachments/assets/5af85bfd-6422-4e50-a6ca-48cd665cc5c7" />
  <img width="1600" height="228" alt="cloud-adain@vaubuntu-getting-started-app$ docker ps" src="https://github.com/user-attachments/assets/fa04e3d0-db6b-445c-90a3-f2989b380fbf" />


### 🛠️ Part 2: Update the Application
* **Action:** Modified the source code and updated the running container.
* **Key Learning:** Learned that containers are immutable; to see changes, you must stop, remove, and rebuild the container.
  
  1. nano src/static/js/app.js
     ```- <p className="text-center">No items yet! Add one above!</p>```
    ```+ <p className="text-center">You have no todo items yet! Add one above!</p>```
  
  <img width="1600" height="228" alt="unknown" src="https://github.com/user-attachments/assets/8d3c1f37-ae74-4571-a14f-c241904ccf7c" />

     Ctrl O, Enter, Ctrl X (To save and exit)
  2. Build your updated version of the image, using the docker build command.
     ```docker build -t getting-started .```
  <img width="1600" height="1242" alt="unknown" src="https://github.com/user-attachments/assets/2564c002-4508-4aa8-be8f-5cd5c467aa97" />
  3. Start a new container to see the updated code
      docker run -d -p 8080:3000 getting-started
      An expected error (See docker workshop part 2 item 3)
     
  <img width="1600" height="358" alt="unknown" src="https://github.com/user-attachments/assets/6ebddbdf-6724-4993-989b-1e711e3cd00b" />

  > [!Note]
  > The old container is currently running and is using the host’s port 3000. Only one process on the machine (including containers) can listen to a specific port. Therefore, the old container must be removed to resolve   this   issue.
  
  5. Remove a container 

  <img width="1600" height="454" alt="unknown" src="https://github.com/user-attachments/assets/a9074ed1-42f6-4c74-8914-393dd1283218" />

  6.  Now run the docker
      - docker run -d -p 8080:3000 getting-started
      - Visit the app on http://34.88.40.199:8080
  <img width="1600" height="992" alt="You have no todo items yet! Add one above" src="https://github.com/user-attachments/assets/db138060-843e-4b5b-94a4-7a144bb4e916" />

### 💾 Part 3: Persist the Database
* **Action:** Initialized a named **Volume** to store the Todo list data.
* **Key Learning:** Discovered how to keep data alive even after a container is deleted by mapping an internal path to a Docker-managed volume.
* **Command:** `docker run -v todo-db:/etc/todos ...`
  
  - Connecting via SSH
  - Open your terminal to SSH into the VM.
  > Note: Since this is an ephemeral VM, restarting it will change the External IP Address. Always check for the new IP in the Google Cloud console before connecting.
  1. Get the new IP: Find the updated External IP in your GCP dashboard.
  2. SSH into the VM:
    ```bash ssh username@NEW_IP_ADDRESS```
  > Note: I finished this during class I have a proof screenshot from last time 
  <img width="1185" height="361" alt="unknown" src="https://github.com/user-attachments/assets/4e90971b-0a2b-48e1-9e35-e3b2b2b3ff2b" />
  3. Redoing this sharing of app, create a repository from docker hub
  <img width="1195" height="812" alt="unknown" src="https://github.com/user-attachments/assets/85af7d52-d3ad-4860-bf8f-bc0064d964c0" />
  4. Push the image
  ```bash docker push docker/getting-started```
  <img width="923" height="423" alt="unknown" src="https://github.com/user-attachments/assets/c94ef251-8a63-43e4-87d0-d7e0f9a63d92" />
  
  Error expected as per workshop:
  
  <img width="894" height="368" alt="unknown" src="https://github.com/user-attachments/assets/8461fccd-d84b-4b22-9a68-fc61ef78d914" />

  5. To fix this, first sign in to Docker Hub using your Docker ID: ```bash docker login YOUR-USER-NAME.```
     
  <img width="894" height="521" alt="unknown" src="https://github.com/user-attachments/assets/0de9312f-2af3-4a26-b6cc-329d43ce172a" />
  
  <img width="894" height="351" alt="unknown" src="https://github.com/user-attachments/assets/05eddee4-1cac-4cc5-afc0-e963c2fec931" />

  7. Testing the Image Share. To confirm the image is available on Docker Hub, simulate a "fresh machine" by deleting your local copy first:
  8. Remove the local image: ```bash docker rmi your-username/getting-started```
  9. Pull it back from Docker Hub: ```bash docker pull your-username/getting-started```
      
  <img width="894" height="228" alt="unknown" src="https://github.com/user-attachments/assets/8f5e20f3-9cf8-4fd1-8823-d892f494294b" />
  
      Run the app: docker run -d -p 8080:3000 getting-started
      Visit the app: http://<ip>
      
<img width="894" height="621" alt="unknown" src="https://github.com/user-attachments/assets/af95415b-2ad7-45aa-a0a7-acf0a43a7939" />


### 📂 Part 4: Use Bind Mounts
* **Action:** Used bind mounts to connect my VM's local filesystem to the container.
* **Key Learning:** Used this for "hot-reloading" during development so changes reflect instantly without a full rebuild.

> [!NOTE]
> Once again we will map from port 8080 on the host and will not restrict traffic to the localhost as we will run this on our Google servers.
  ```bash docker run -dp 8080:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started```

1. Start an Alpine container and create a new file in it.
<img width="908" height="204" alt="unknown" src="https://github.com/user-attachments/assets/a63c7877-2c1d-4c1a-a40a-b43f76985f58" />

2. Run a new Alpine container and use the stat command to check whether the file exists.
<img width="880" height="84" alt="unknown" src="https://github.com/user-attachments/assets/bb105ca9-0783-4cfc-be44-47c8055047e1" />

> [!NOTE]
> Volumes provide the ability to connect specific filesystem paths of the container back to the host machine. If you mount a directory in the container,
> changes in that directory are also seen on the host machine. If you > mount that same directory across container restarts, you'd see the same files.

3. Persist the todo data (Create a volume and start the container)
    Create a volume and start the container
    Create a volume by using the ```bash docker volume create``` command.
    Stop and remove the todo app container once again with ```bash docker rm -f <id>```, as it is still running without using the persistent volume.

<img width="880" height="247" alt="unknown" src="https://github.com/user-attachments/assets/d4cd62e2-123f-447e-ab9c-0d3782b1306e" />

4. Start the todo app container, but add the --mount option to specify a volume mount. Give the volume a name, and mount it to /etc/todos in the container, which captures all files created at the path.
```bash docker run -dp 8080:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started```

<img width="880" height="106" alt="unknown" src="https://github.com/user-attachments/assets/74621356-9e28-479a-907b-d12bdb31f65a" />

* Verify that the data persists
1. Once the container starts up, open the app and add a few items to your todo list. Visit the app: http://<ext ip>

<img width="880" height="759" alt="unknown" src="https://github.com/user-attachments/assets/bb84cc2e-762c-47f8-9003-416e399e1462" />

2. Stop and remove the container for the todo app. Use Docker Desktop or docker ps to get the ID and then docker rm -f <id> to remove it.

<img width="887" height="203" alt="unknown" src="https://github.com/user-attachments/assets/8da11fe5-1d8f-4c87-bacf-c55192324d98" />

4. Start a new container using the previous steps. ```bash docker run -dp 8080:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started```

5. Open the app. You should see your items still in your list.

<img width="1316" height="820" alt="unknown" src="https://github.com/user-attachments/assets/4823c46e-f54a-4b6c-88ef-7b86161eb8c1" />

7. Go ahead and remove the container when you're done checking out your list.
   
<img width="973" height="206" alt="unknown" src="https://github.com/user-attachments/assets/7318d58f-4de8-4fc4-b447-13bf39250b60" />

> [!Note]
> A lot of people frequently ask "Where is Docker storing my data when I use a volume?" If you want to know, you can use the docker volume inspect command.
<img width="973" height="331" alt="ras na 50-278-2638 ," src="https://github.com/user-attachments/assets/ecc4b3db-abbc-4bff-8d90-02ebc64582ca" />

### 🌐 Part 5: Multi-Container Apps
* **Action:** Created a Docker Network to link a MySQL container with the App container.
* **Key Learning:** Containers can communicate via **Service Names** within the same network, keeping the database isolated from the public internet.
  
> [!Note]
> A bind mount is another type of mount, which lets you share a directory from the host's filesystem into the container. When working on an application, you can use a bind mount to mount source code into the container.
> The container sees the changes you make to the code immediately, as soon as you save a file. This means that you can run processes in the container that watch for filesystem changes and respond to them.
> [!Warning]
> Note: Skip the "File Sharing" Setting instruction is strictly for Windows/Mac users. On your Ubuntu VM, Docker has native access to the filesystem. No need to check any GUI settings or "turn on" sharing.
1. Ensure you are currently inside the app directory:
<img width="577" height="158" alt="unknown" src="https://github.com/user-attachments/assets/e59794f0-2079-47d9-b418-20d9ab52dc7c" />

2. Perform the "Trying out bind mounts”. Run the following command to start bash in an ubuntu container with a bind mount. Inside the VM:
   ```bash docker run -it --mount type=bind,src=.,target=/src ubuntu bash```
<img width="893" height="225" alt="unknown" src="https://github.com/user-attachments/assets/f0e9ab98-51cf-4442-ac25-81c3f18602a6" />

3. Change directory to the src directory.
4. Create a new file named myfile.txt.

<img width="893" height="167" alt="root@6baf041ebcefarcarct cd arc" src="https://github.com/user-attachments/assets/a888eb04-73a0-4520-ba6a-2cf90f89e5ff" />

5. Open the getting-started-app directory on the host and observe that the myfile.txt file is in the directory.
    Exit the container type: exit
    On GCP VM terminal, type: ls
   
<img width="893" height="119" alt="unknown" src="https://github.com/user-attachments/assets/fa1a3aa9-b966-459a-a804-37f79ca25669" />

6. From the host, delete the myfile.txt file. (Item 8 from docker workshop). From the gcp vm terminal, run: rm myfile.txt

<img width="893" height="217" alt="unknown" src="https://github.com/user-attachments/assets/b1b6f64d-a587-4dfd-a968-b9a4e957b61b" />

7. In the container, list the contents of the app directory once more.
   Run command: docker run -it --rm --mount type=bind,src=.,target=/src ubuntu bash
   
<img width="893" height="217" alt="unknown" src="https://github.com/user-attachments/assets/22fa8eb1-f220-43fd-8a64-251a7880e4b0" />

> [!Note]
> In the container, list the contents of the app directory once more. Observe that the file is now gone.

<img width="743" height="73" alt="unknown" src="https://github.com/user-attachments/assets/2d34db3d-e566-4ae5-9c9c-92064f1e0fc5" />

Stop the interactive container session with Ctrl + D.

> [!Note]
> This procedure demonstrated how files are shared between the host and the container, and how changes are immediately reflected on both sides.
> Now you can use bind mounts to develop software.

### 🏗️ Part 6: Use Docker Compose
* **Action:** Consolidated all configurations into a single `docker-compose.yaml` file.
* **Key Learning:** Orchestration allows for "Infrastructure as Code," making it easy to start the entire stack with one command.
* **Command:** `docker compose up -d`

> [!Note]
> Container networking
> Remember that containers, by default, run in isolation and don't know anything about other processes or containers on the same machine.
> So, how do you allow one container to talk to another? The answer is networking. If you place the two containers on the same network, they can talk to each other.

**Start MySQL**

There are two ways to put a container on a network:
Assign the network when starting the container.
Connect an already running container to a network.
In the following steps, you'll create the network first and then attach the MySQL container at startup.
1. Create the network.
  In gcp terminal, run command: docker network create todo-app

<img width="865" height="52" alt="unknown" src="https://github.com/user-attachments/assets/60cfb78e-ad05-4dd4-9fc2-7b67da6dbf04" />

2. Now, run this long command to start the database.
   
   ```bash
   docker run -d \
    --network todo-app --network-alias mysql \
    -v todo-mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=todos \
    mysql:8.0```

<img width="886" height="631" alt="unknown" src="https://github.com/user-attachments/assets/a4d98185-168d-4ad6-96ac-429a0bbbbd90" />

> [!Note]
> Note to ensure database is actually running on your VM, type: docker ps
> It should show a container using the mysql:8.0 image with a status of "Up."

<img width="886" height="154" alt="unknown" src="https://github.com/user-attachments/assets/ba2161b8-6127-4fd7-842a-639fbb0f296b" />

3. To confirm you have the database up and running, connect to the database and verify that it connects.
   
  docker exec -it <mysql-container-id> mysql -p

<img width="886" height="434" alt="unknown" src="https://github.com/user-attachments/assets/d0417411-4cc4-49ca-8122-a4ae323094ea" />

  - When the password prompt comes up, type in secret. In the MySQL shell, list the databases and verify you see the todos database.
  - From the command line: mysql> SHOW DATABASES;

<img width="886" height="330" alt="unknown" src="https://github.com/user-attachments/assets/1d1cff15-332e-407e-8382-c292443e3ae0" />

**Connect to MySQL**
> [!Note]
> We are going to use nicolaka/netshootcontainer, which ships with a lot of tools that are useful for troubleshooting or debugging networking issues.

  1. Start a new container using the nicolaka/netshoot image. Make sure to connect it to the same network. ```bash docker run -it --network todo-app nicolaka/netshoot```
  2. Inside the container, you're going to use the dig command, which is a useful DNS tool. You're going to look up the IP address for the hostname mysql.

  <img width="886" height="930" alt="unknown" src="https://github.com/user-attachments/assets/d8833aad-2b0e-49cb-a545-a6e798f043af" />

  3. To find IP Address: dig mysql

  <img width="790" height="542" alt="unknown" src="https://github.com/user-attachments/assets/ca6ca27a-4c37-4dc8-8c23-45920cc31be0" />

**You can now start your dev-ready container.**
  1. Specify each of the previous environment variables, as well as connect the container to your app network.
     Make sure that you are in the getting-started-app directory when you run this command.
  Note: Ensure we are on 8080:3000

  <img width="891" height="375" alt="unknown" src="https://github.com/user-attachments/assets/12968a80-712f-4947-abdc-bb856415882a" />

  2. If you look at the logs for the container (docker logs -f <container-id>), you should see a message similar to the following, which indicates it's using the mysql database.
     From the command line:  docker logs -f ee55

  <img width="891" height="345" alt="unknown" src="https://github.com/user-attachments/assets/3a9cc7f9-f8c5-46a4-a183-87b2a128f6f0" />

  3. Open the app in your browser and add a few items to your todo list. Visit: http://<ip>

  <img width="745" height="416" alt="unknown" src="https://github.com/user-attachments/assets/41beb7f5-69bd-4c36-93fb-d6449313ff45" />
  
  4. Connect to the mysql database and prove that the items are being written to the database. Remember, the password is secret.
     docker exec -it 39bd8baef51e mysql -p todos
     
  <img width="914" height="485" alt="unknown" src="https://github.com/user-attachments/assets/c1f85069-8f5d-4722-bd70-74742d2c1009" />

  And in the mysql shell, run the following: mysql> select * from todo_items;

  <img width="914" height="469" alt="unknown" src="https://github.com/user-attachments/assets/16aa58da-84fa-4852-b291-443432aa6ad5" />

> [!Note]
> Dev / local / testing → Feel free to use plain ENV vars (quick & easy).
> Production → Switch to proper secrets management → mount as files → use the _FILE env vars if your image supports them.
> This follows security best practices and reduces the chance of accidentally exposing credentials through logs, debugging, or compromised containers.
> The blog post by Diogo Mónica is still considered a classic reference on this topic — it's worth reading if you want the full security rationale (it's short and very clear).

### 🚀 Part 7: Deployment (GCP VM)
* **Action:** Deployed the application on a Google Cloud Compute Engine instance.
* **Key Learning:** Managed "Deployment Links" by configuring GCP Firewall rules (Port 8080) and handling dynamic External IP changes after VM restarts.
* **Status:** Successfully verified via `curl http://localhost:8080` and external browser access.

> [!Note]
> Docker Compose is a tool that helps you define and share multi-container applications. With Compose, you can create a YAML file to define the services and with a single command,
> you can spin everything up or tear it all down.

**Create the Compose file**

- In the getting-started-app directory, create a file named compose.yaml.
- Ensure the vm terminal is in getting-started-app
- Then: nano compose.yaml
- As per workshop: Define this service in the compose.yaml file.

<img width="785" height="691" alt="unknown" src="https://github.com/user-attachments/assets/acdb8283-5b6a-4200-8ef5-6a6a65939880" />

- Save and exit: Ctrl O and then Enter to save, Ctrl X 
- Verify compose.yaml is created and save: ls and nano compose.yaml

**Just a note from compose.yaml**

<img width="679" height="542" alt="unknown" src="https://github.com/user-attachments/assets/755ca7ea-9d25-4afe-b9b8-de6f76d305ce" />

1. Launch thr stack:
> [!Note:]
> If there are existing containers, networks, or ports still running in the background, they may cause conflicts when starting the workshop setup.
> Before continuing, make sure no other copies of the containers are   running. Use:

- docker ps to list currently running containers
- docker rm -f <container_id> to stop and remove any that are running
- Run this command: docker rm -f <node-id> <mysql-id>

<img width="898" height="125" alt="unknown" src="https://github.com/user-attachments/assets/67aba7df-7c82-44c3-9ecd-547057666491" />

2. Start up the application stack using the docker compose up command. Add the -d flag to run everything in the background.
docker compose up -d

<img width="898" height="184" alt="unknown" src="https://github.com/user-attachments/assets/b9b24d46-74b3-4133-8914-6faed4adcf5a" />

3. Look at the logs using the docker compose logs -f command. You'll see the logs from each of the services interleaved into a single stream. This is incredibly useful when you want to watch for timing-related issues. The -f flag follows the log, so will give you live output as it's generated.

<img width="898" height="737" alt="nysql-1" src="https://github.com/user-attachments/assets/0768ed88-23b1-4e17-a275-d82ea8e14554" />

4. At this point, you should be able to open your app in your browser on http://<ip> and see it running.

<img width="621" height="344" alt="unknown" src="https://github.com/user-attachments/assets/fffdd138-0540-4995-ab43-54a5e8e9744a" />


Finally, push your code to Github

First: ssh-keygen -t ed25519 -C "your-github-email@example.com"

Having an error:

<img width="872" height="424" alt="unknown" src="https://github.com/user-attachments/assets/46353e15-4374-4649-8dbd-e7784a033adf" />

To fix error, pull the changes from GitHub
git pull origin main

<img width="872" height="351" alt="unknown" src="https://github.com/user-attachments/assets/59e64794-2ef1-43c3-8a00-a78a1ea58272" />

Now: git push origin main (Need to ssh again on my github for some reason)

<img width="718" height="962" alt="unknown" src="https://github.com/user-attachments/assets/cfc76892-cf50-4f6a-bf69-92bb665851b6" />


## Docker Workshop Overview
The following steps outline the process to restore the multi-container environment after the GCP VM (`vmubuntu`) has been stopped. This procedure ensures the application defined in `docker-compose.yml` is correctly initialized and accessible.

---

## Step 1: Instance Initialization
1.  **Start the VM:** Log in to the Google Cloud Console and start the `vmubuntu` instance.
2.  **Identify External IP:** Note the newly generated **External IP address** (GCP typically assigns a new ephemeral IP upon restart).

## Step 2: Establish SSH Connection
Access the VM via your terminal or SSH client using the updated IP:
```bash ssh <your-username>@<new-external-ip>```

## Step 3: Deployment Multi-Container Application
Access the VM via your terminal or SSH client using the updated IP:
### Navigate to the project root
cd ~/getting-started-app

### Launch containers in detached mode
docker compose up -d

### Verify all containers are running (Status: Up)
docker ps -a

## Step 4: Verification & Deployment Links
curl http://localhost:8080

External Access: Open your local web browser and navigate to:
http://<newexternal-ip>:8080

<img width="931" height="348" alt="image" src="https://github.com/user-attachments/assets/9158a8aa-6d37-4de0-bb7e-4820dddcd3d2" />


Note: Ensure that the GCP Firewall rules still allow incoming traffic on port 8080.

<img width="962" height="276" alt="image" src="https://github.com/user-attachments/assets/6d4ef9c5-2773-4a79-aa02-a2254cea84d3" />

Visit the app  http://35.228.250.108:8080

>[!Note]
> Dont forget to push changes to github.
## Step 5: Version Control & Persistence
To ensure code changes are backed up and versioned, the following Git workflow was used:

1. *Staging:* `git add .` to prepare changes.
2. *Commit:* `git commit -m "Update deployment configuration"` to log the change.
3. *Push:* `git push origin main` to sync the VM environment with the GitHub repository.

**Tear it all down
When you're ready to tear it all down, simply run docker compose down or hit the trash can on the Docker Desktop Dashboard for the entire app. 
The containers will stop and the network will be removed.**






