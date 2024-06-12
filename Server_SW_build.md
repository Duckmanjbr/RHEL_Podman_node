## Configuration setup:

### Set static IP
1. `sudo nmtui`

### Name the server
1. `sudo hostnamectl set-hostname {name}`

### Set timezone and verify time is being syncd from NTP 
1. `sudo timedatectl set-timezone UTC`
2. `sudo vi /etc/chrony.conf`
3. `sudo systemctl restart chronyd`
4. `sudo timedatectl status` and `sudo chronyc sources`

### Create folder structure for containers/VMs
1. 'mkdir /home/duckman/containers /home/duckman/vms'
2. 'mkdir /home/duckman/containers/pihole /home/duckman/containers/unifi'

### Update server and install baseline
1. 'sudo dnf update -y'
2. 'curl -LO https://github.com/docker/compose/releases/download/v2.27.0/docker-compose-linux-x86_64'
3. 'chmod +x docker-compose-linux-x86_64'
4. 'sudo mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose'
5. 'sudo dnf -y install podman podman-docker virt-v2v dnf-plugins-core'
6. 'sudo ln -s /usr/libexec/docker/cli-plugins/docker-compose /usr/local/bin/docker-compose'

### Setup Podman
1. 'sudo systemctl enable --now podman.socket'
2. 'systemctl --user enable --now podman.socket'
3. We also need to define and export the DOCKER_HOST environment variable. The traditional way to do this is by adding the line below to ~/.bash_profile or ~/.profile, depending on the shell we are using:
'export DOCKER_HOST=unix:///run/user/1000/docker.sock'
4. 'source ~/.bash_profile'
