## Prerequisites: 
### A. Sign up to google cloud student

### B. Create a VM using Google Cloud Platform
Virtual Machine that runs ubuntu 

1. Go to google cloud homepage click the create VM 
2. Machine Configuration
    - Name the instance e.g myvm
    - Set Region for latency anywhere close Europe, Any Zone
    - Select E2 by default, it default to the cheapest
    - Provision model: Standard (this is currently the value by default)
<img width="1452" height="1022" alt="•00•00000000" src="https://github.com/user-attachments/assets/2f1fd665-ed54-4f20-9f00-531b5bd5d116" />

3. OS and storage: 
  From Operating system and storage. Edit to change it to:
    - OS: Ubuntu
    - Version: x86/64, amd64 questing minimal image built on 2026-02-25 
    - Then click Select to save changes
<img width="1293" height="644" alt="unknown" src="https://github.com/user-attachments/assets/d08af22a-07fa-4548-a59f-2ac1173aeca0" />


Select to save the OS version settings

<img width="783" height="607" alt="unknown" src="https://github.com/user-attachments/assets/a7401c12-a565-44d6-b841-4ff72fcff521" />

4. Data protection: Default set-up is fine
5. Networking: Allow http-server and https-server
6. Observability: Leave default value
7. Security > Manage access add item > add ssh key

Generate a new ssh key on you machine
Generate a new ssh key

### Generate a new ssh key
ssh-keygen -t ed25519 -f .ssh/my_key
### Print the pubkey (copy to VM ssh keys)
cat .ssh/my_key.pub 

Note: Since this is ephemeral external ip can change 

After pasting the new ssh key click Create 
Now connect to the VM from terminal/shell

### Connect to the VM using the key name you set when adding SSH key. 
Note you can replace user@macbook from the end of the long ssh key string to e.g cloud-admin

ssh -i .ssh/vm_key cloud-admin@<externalip>
<img width="1345" height="1600" alt="27 maritesablena@Maritess-KacBook-Air Locat" src="https://github.com/user-attachments/assets/f4d3658a-63ea-4829-b467-d1fa0041229c" />

> [!IMPORTANT]  
> **Super Important Step – Do this BEFORE installing Docker!**  
> Your website/container won't appear in the browser if the VM blocks the traffic.

### Open the port on your cloud provider (NOT inside the VM or Docker)
Go to your cloud dashboard (before or right after creating the VM):
- **Google Cloud (GCP)** → Click your VM → **Networking** tab → Add or edit firewall rule  
Add a rule like this (example for a simple website):
- **Type / Protocol**: TCP  
- **Port range**: 80  
  (use 8080, 3000, 5000 etc. if your app uses a different port)  
- **Source / Anywhere**: 0.0.0.0/0  
  → This means "allow from the whole internet"  
  ⚠️ **Only do this for learning/workshop!** In real projects, change it to **your own IP** only for safety.
  

### C. Install Docker via GCP VM
Inside the VM to install Docker from https://docs.docker.com/engine/install/ubuntu/. 

1. As per notes: Please install using the "install using apt" on your virtual machine.
   <img width="1407" height="994" alt="unknown" src="https://github.com/user-attachments/assets/8d2a7f24-fe52-44a1-bc99-ce409cc2d847" />

   <img width="1461" height="1600" alt="unknown" src="https://github.com/user-attachments/assets/fbda55eb-198c-47aa-ae72-b2eb208e9072" />

  sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
2. sudo usermod -aG docker `whoami`
3. Then logout/login
<img width="1600" height="1571" alt="unknown" src="https://github.com/user-attachments/assets/7f59e3fc-65c7-42b9-9d76-90d20dea59d6" />

<img width="1600" height="1356" alt="unknown" src="https://github.com/user-attachments/assets/80ab4a6a-acb0-4e15-9109-82829a4a4767" />


## Proceed to workshop
https://docs.docker.com/get-started/workshop/02_our_app/
See my completed docker workshop https://github.com/diovsset/getting-started-app/blob/main/workshop.md



    
