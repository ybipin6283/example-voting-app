Pre-check!
- create a server for self hosted agent
- create the ACR to keep the images 
- Create the AKS cluster for the application host
    - install the argocd
    - configure the argocd for the
- all the pipeline yaml code given in the same repo.



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
🧪 Step 3: Test Docker Manually
``` bash
whoami              # should show: azadmin
docker ps           # should NOT give 'permission denied'
```
🔄 Step 4: Reinstall Azure DevOps Agent as azadmin (CRITICAL)
``` bash
cd ~/myagent   # Or wherever your agent is installed
./svc.sh stop
./svc.sh uninstall
```
Reconfigure agent:
``` bash
./config.sh   # Run this as the `azadmin` user!
```
Reinstall service:
``` bash
./svc.sh install
./svc.sh start
```
🟢 Final Confirmation
``` bash
groups azadmin
```
It must show:
``` bash
azadmin : azadmin sudo docker
```
