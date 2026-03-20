Docker Workshop: Getting Started

This repository is a personal fork of the Docker Getting Started App. It serves as a hands-on lab environment for completing the official Docker Workshop.

Reference Material
Official Workshop Guide: Docker Workshop Documentation
Original Repository: docker/getting-started

Infrastructure Setup
Before diving into Docker, the following environment was provisioned to host the application:

Prerequisites
- Sign up to google cloud to get the student one
- Environment: A dedicated Compute Engine VM running Ubuntu.

Deployment Steps
VM Provisioning: Setup and configuration of the Ubuntu instance on GCP.
Access Control: Configured SSH access for secure remote management.
Note: For detailed steps on how the VM was configured, see my Create VM documentation via gcp
Docker Installation: --> briefly mention if you installed Docker via script or manual commands here..

Progress Tracking
I am documenting my journey through the workshop modules below:

[ ] Part 1: Containerize an application
  1. Fork the repository rather than cloning, as this avoids the need to push back from the server
     <img width="902" height="208" alt="unknown" src="https://github.com/user-attachments/assets/ffcf4ee6-cc6a-456c-b660-dd579f9cd3b7" />
  2. After forking the repository, clone it inside the VM.
  <img width="1600" height="428" alt="unknown" src="https://github.com/user-attachments/assets/8c14b9de-f2a6-4f58-a402-7e7d1337f8a4" />
  <img width="1600" height="216" alt="unknown" src="https://github.com/user-attachments/assets/ae50e17a-b283-4691-b27f-ee90c4049bab" />

  Verify the cloned repository by navigating into the directory and listing its contents:
      cd getting-started
      ls -a
  <img width="1600" height="847" alt="unknown" src="https://github.com/user-attachments/assets/b19c8a23-575c-45a0-93d0-83ce0546b575" />

"Note: The forked repository already contained a Dockerfile. To follow the workshop from scratch, I cleared the existing file using nano Dockerfile and replaced the content with the official workshop instructions."

<img width="1600" height="1321" alt="unknown" src="https://github.com/user-attachments/assets/ad0e3c22-ed67-45b7-8092-0aea08b907c1" />

  3. Clear the existing Dockerfile and paste the following content inside (see Docker Workshop Vuild the App Image step 1)
<img width="1600" height="785" alt="unknown" src="https://github.com/user-attachments/assets/98f2931e-d141-4134-86ac-fa32b366633a" />
  Saving and Exiting (Nano Editor)
  If you are using the nano editor on your VM, follow these steps to save your changes:
    - Save: Press Control + O (Write Out).
    - Confirm: Press Enter to keep the filename as Dockerfile.
    - Exit: Press Control + X to return to the command line.
  4. Build the Image. Once the file is saved, use the following command to build your Docker image:
     ```docker build -t getting-started .```
  Result:
  <img width="1600" height="1269" alt="unknown" src="https://github.com/user-attachments/assets/edcc4487-5bc2-401e-81a9-f624b5ad6ffb" />
  5. Run your container using the ```docker run``` command and specify the name of the image you just created:
     ```docker run -d -p 8080:3000 getting-started```
     <img width="1600" height="129" alt="Loud-adminivaabuntu-getting-started-appdocker run -d p 80803000 getting-started" src="https://github.com/user-attachments/assets/18a799ef-804e-4342-942a-92416b0c326c" />
  6. Visit the app on http://<extip>
  <img width="778" height="464" alt="Not Secure - 34840 199" src="https://github.com/user-attachments/assets/5af85bfd-6422-4e50-a6ca-48cd665cc5c7" />
  <img width="1600" height="228" alt="cloud-adain@vaubuntu-getting-started-app$ docker ps" src="https://github.com/user-attachments/assets/fa04e3d0-db6b-445c-90a3-f2989b380fbf" />


[ ] Part 2: Update the application (Update the source code)
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

  "The old container is currently running and is using the host’s port 3000. Only one process on the machine (including containers) can listen to a specific port. Therefore, the old container must be removed to resolve this   issue."
  5. Remove a container v
    <img width="1600" height="454" alt="unknown" src="https://github.com/user-attachments/assets/0c7c0049-f8c6-46e3-9319-d1b39afa9334" />
  6.  Now run the docker
      - docker run -d -p 8080:3000 getting-started
      - Visit the app on http://34.88.40.199:8080
  <img width="1600" height="992" alt="You have no todo items yet! Add one above" src="https://github.com/user-attachments/assets/db138060-843e-4b5b-94a4-7a144bb4e916" />




[ ] Part 3: Updating our App

[ ] Part 4: Sharing our App (Docker Hub)

[ ] Part 5: Persisting our DB (Volumes)
