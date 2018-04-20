*How to copy SSH keys and K8s config from Azure Linux VM](./CopyFromLinuxVM.md)

Sample script for Windows using Putty tools  
  
Replace <VM_IP> with VM fqdn or IP  

pscp -r gab18usr@<VM_IP>:/home/gab18usr/.kube/ %USERPROFILE%/kube/
pscp -r gab18usr@<VM_IP>:/home/gab18usr/.ssh/ %USERPROFILE%/ssh/
pscp -r gab18usr@<VM_IP>:/home/gab18usr/.azure/ %USERPROFILE%/azure