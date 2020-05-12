FROM centos:8

# Core deps
RUN yum install -y epel-release passwd wget diffutils;\
    yum install -y python36 file bzip2 unzip bc jq tmux nmap-ncat glibc.i686 libstdc++.i686 ncurses

# Setup non root user
RUN useradd -m gsm
RUN < /dev/urandom tr -dc _A-Z-a-z-0-9 | head -c${1:-32} | passwd --stdin gsm

# Switch to non root user
USER gsm
WORKDIR /home/gsm

# Create custom directories
RUN mkdir -p /home/gsm/serverfiles/saves ;\
    mkdir -p /home/gsm/serverfiles/mods ;\
    mkdir -p /home/gsm/lgsm/config-default/config-game ;\
    mkdir -p /home/gsm/lgsm/config-default/config-lgsm

# Install linuxGSM
RUN wget -O linuxgsm.sh https://linuxgsm.sh ;\
    chmod +x linuxgsm.sh

# Pre-install game control files
# Stationeers
RUN ./linuxgsm.sh stserver

# Default entrance
ENTRYPOINT ["tail","-f","/dev/null"]