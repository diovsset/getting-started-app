* Docker Workshop: Getting Started

* This repository is a personal fork of the Docker Getting Started App. It serves as a hands-on lab environment for completing the official Docker Workshop.

Reference Material
Official Workshop Guide: Docker Workshop Documentation
Original Repository: docker/getting-started

* Prerequisites
- Sign up to google cloud to get the student one
- Environment: A dedicated Compute Engine VM running Ubuntu.

* Deployment Steps
VM Provisioning: Setup and configuration of the Ubuntu instance on GCP.
Access Control: Configured SSH access for secure remote management.
Note: For detailed steps on how the VM was configured, see my Create VM documentation via gcp
Docker Installation: --> briefly mention if you installed Docker via script or manual commands here..

* Progress Tracking
I am documenting my journey through the workshop modules below:

> [!TIP] 
> Part 1: Containerize an application
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


> [!TIP] 
> Part 2: Update the application (Update the source code)
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

> [!TIP] 
> Part 3: Share the application (Docker Hub)
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


> [!TIP] 
> Part 4: Persists the DB

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

> [!TIP]
> Part 5: Use bind mounts
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
> >In the container, list the contents of the app directory once more. Observe that the file is now gone.

<img width="743" height="73" alt="unknown" src="https://github.com/user-attachments/assets/2d34db3d-e566-4ae5-9c9c-92064f1e0fc5" />

Stop the interactive container session with Ctrl + D.
> [!Note] This procedure demonstrated how files are shared between the host and the container, and how changes are immediately reflected on both sides.
> Now you can use bind mounts to develop software.

> [!TIP]
> Part 5: Multi container apps




> [!TIP]
> Part 5: Persisting our DB (Volumes)
