
## Setting up T2
    scp -i "AWSParis.pem" ~/.ssh/id_rsa centos@ec2-35-180-63-143.eu-west-3.compute.amazonaws.com:~/
    ssh -i "AWSParis.pem" centos@ec2-35-180-63-143.eu-west-3.compute.amazonaws.com
    mv id_rsa ~/.ssh/
    sudo yum install -y vim-enhanced
    eval `ssh-agent`
    ssh-add ~/.ssh/id_rsa
    git clone git@github.com:sgnoohc/dot.git
    curl https://raw.githubusercontent.com/Shougo/neobundle.vim/master/bin/install.sh > install.sh; sh install.sh;
    cd dot/
    source setup.sh
    git clone https://github.com/aws/aws-fpga.git $AWS_FPGA_REPO_DIR
    sudo yum install -y xauth
    sudo yum install -y xclock
    sudo yum install -y xorg-x11-server-Xorg xorg-x11-xauth xorg-x11-apps
    cd $AWS_FPGA_REPO_DIR; source sdaccel_setup.sh
    sudo yum update -y java
# aws-fpga-notes
