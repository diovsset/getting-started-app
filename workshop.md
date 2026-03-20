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

[ ] Part 1: Getting Started (Setup & Installation)
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
  6. Visit the app on http://<ext ip>
    <img width="778" height="464" alt="unknown" src="https://github.com/user-attachments/assets/78b1317e-1f48-4187-8be1-0ace29fc24ae" />

    <img width="1600" height="228" alt="unknown" src="https://github.com/user-attachments/assets/ef89d9c6-a576-4605-9edf-9bed28fc26f9" />


[ ] Part 2: Our Application (Building the Image)

[ ] Part 3: Updating our App

[ ] Part 4: Sharing our App (Docker Hub)

[ ] Part 5: Persisting our DB (Volumes)
