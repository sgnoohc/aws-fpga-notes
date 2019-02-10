
## Setting up T2
    sudo yum install -y vim-enhanced
    curl https://raw.githubusercontent.com/Shougo/neobundle.vim/master/bin/install.sh > install.sh; sh install.sh;
    git clone git@github.com:sgnoohc/dot.git
    source setup.sh
    git clone https://github.com/aws/aws-fpga.git $AWS_FPGA_REPO_DIR
    sudo yum install xauth
    sudo yum install xclock
    sudo yum groupinstall "X Window System"
    sudo yum install -y xorg-x11-server-Xorg xorg-x11-xauth xorg-x11-apps
    source sdaccel_setup.sh
    sudo yum update java
# aws-fpga-notes
