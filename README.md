Steps to display nvme ssd temperature on conky display (Ubuntu 24.04)

1. Install nvme-cli
   Install it using command `sudo apt install nvme-cli`. Check if it installed correctly by running command `sudo nvme smart-log /dev/nvme0`. It will show the information about the nvme device `nvme0` in your pc.
2. Make it able to run without password
   Since the command `smart-log` require sudo. We need to make it run without asking for password when conky executed it. It can be achieved by setting NOPASSWD for the command.
   Add this line to sudoers file:
   `yourusername    ALL=(ALL) NOPASSWD: /usr/sbin/nvme smart-log /dev/nvme0`
3. Edit conky.config file
   Add this line to conky.config file: `${execi 30 sudo nvme smart-log /dev/nvme0 | awk '/^temperature/ {print "NVMe Temp: " $3 "°C"}'}`
