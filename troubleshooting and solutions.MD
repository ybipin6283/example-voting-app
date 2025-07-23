Ultimate Root Cause (RCA):
Your Azure DevOps agent is running as a user that is NOT in the docker group, or Docker is not properly exposed to that user.
🔁 Step 1: Add Agent User to docker Group
``` bash 
sudo usermod -aG docker azadmin
```
🔄 Step 2: Restart the Agent Machine (or Log Out and Back In)
``` bash
sudo reboot 
```
