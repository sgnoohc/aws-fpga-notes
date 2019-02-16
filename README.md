## Setting up t2.xlarge

I use EBS of ~50 GB. the "src/project_data" is the area where the EBS sits. So place your stuff there, otherwise the home area gets cluttered real fast.

    ssh -i AWS.pem centos@ec2-34-220-26-211.us-west-2.compute.amazonaws.com
    source <(curl -s https://s3.amazonaws.com/aws-fpga-developer-ami/1.5.0/Scripts/setup_gui.sh)
    # The above command creates a temporary passwords for 'centos' user so that one can log in via remote desktop
    # Write the password down somewhere else (TODO figure out how to change the password)
    git clone https://github.com/aws/aws-fpga.git $AWS_FPGA_REPO_DIR  
    cd $AWS_FPGA_REPO_DIR                                         
    source sdaccel_setup.sh
    # Above probably will quit your session... Not sure exactly why
    # So login again and run again
    ssh -i AWS.pem centos@ec2-34-220-26-211.us-west-2.compute.amazonaws.com
    cd $AWS_FPGA_REPO_DIR                                         
    source sdaccel_setup.sh

When running the last ```source sdaccel_setup.sh``` command, when it tries to apply AR7... whatever patch it quits due to not being sudo.
I don't know what is going on exactly... But I just login again, and run the command again and it seems to finish just fine the second time.
I also tried running the command with sudo, but that actually messes up your setup. So just run as "centos".
    
    # Separate local session while above is happening
    scp -i AWS.pem ~/.ssh/id_rsa centos@ec2-34-220-26-211.us-west-2.compute.amazonaws.com:~/
    ssh -i AWS.pem centos@ec2-34-220-26-211.us-west-2.compute.amazonaws.com
    mv id_rsa ~/.ssh/
    
    # And to not type password every time do the following so github doesn't ask for passwords constantly
    eval `ssh-agent`
    ssh-add ~/.ssh/id_rsa
    git clone git@github.com:sgnoohc/dot.git
    cd dot/
    source setup.sh
    chmod 600 .ssh/config # TODO I should add this to dot/setup.sh
    
    # Checking out project source codes
    eval `ssh-agent`
    ssh-add ~/.ssh/id_rsa
    cd src/project_data
    git clone git@github.com:sgnoohc/fpga-aws-projects.git
    
## Connecting to Remote Desktop (RDP)

I use [microsoft RDP](https://itunes.apple.com/us/app/microsoft-remote-desktop-8/id715768417?mt=12), which seems to work just fine.
From the RDP app, add the IP address: 34.220.26.211, then connect, and use 'centos' user plus the temprorary password generated from the step involving the command ```source <(curl -s https://s3.amazonaws.com/aws-fpga-developer-ami/1.5.0/Scripts/setup_gui.sh)```

## Checking setup status

Just few checks to see if things behave normally...
Check whether the GUI works fine for SDAccel and Vivado

    # Log in via RDP following instructions from previous section
    # Then after logging in fire up the Terminal from the icon at the top of the menu bar in linux desktop
    
    sdx # check if it opens OK
    
    
## RTL Kernel Wizard

RTL Kernel Wizard sets you up with RTL Kernel template vivado project.
The peripherals defined from the RTL Kernel Wizard takes care of the basic kernel requirements for you and generate I/O related codes.
So the user can focus on adding the core kernel functions only.
To use GUI it is best to use the RDP connection described in previous section.

    # Assuming you are logged into RDP
    # Click at the icon that looks like a terminal at the top of the desktop
    # Then in the terminal issue the following command to start the SDAccel gui
    cd $AWS_FPGA_REPO_DIR                                         
    source sdaccel_setup.sh
    sdx # if works fine close
    vivado # if works fine then close
    # if asked to set the workspace set it to ~/src/project_data/workspace # if directory does not exist create one
    
    
Set the workspace to be under /home/centos/src/project_data/workspace, because ~/src/project_data is where your EBS is mounted on, and therefore has large disk space.
Click Create SDx Project
Select Application
Create Project name
Add Platform
Select /home/centos/src/project_data/aws-fpga/SDAccel/aws_platform/xilinx_aws-vu9p-f1-04261818_dynamic_5_0
OK
Next. Next.
Empty Application
Finish
At the top, from the menubar, Xilinx->RTL Kernel Wizard...
If running for the first time, wait a while... it takes time.
There are 5 steps.
Some info displayed. Click Next
Set the Kernel name. (Choose wisely. and do not choose poorly.)
Choose various things and once you finish this step, you'll get a Vivado project opened in Vivado. (Yay, the familiar Vivado and not this SDAccel thing...)

## Setting up t2.* instances (BAD) (Deprecated old way)
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
    sudo yum install -y xorg-x11-server-Xorg xorg-x11-xauth xorg-x11-apps xclock
    cd $AWS_FPGA_REPO_DIR; source sdaccel_setup.sh
    sudo yum update -y java
## Just use https://www.xilinx.com/products/design-tools/acceleration-zone/aws.html#gettingstarted

## Setting up t2.xlarge

    source <(curl -s https://s3.amazonaws.com/aws-fpga-developer-ami/1.5.0/Scripts/setup_gui.sh)
    git clone https://github.com/aws/aws-fpga.git $AWS_FPGA_REPO_DIR  
    cd $AWS_FPGA_REPO_DIR                                         
    source sdaccel_setup.sh
    
    # Separate local session while above is happening
    scp -i AWS.pem ~/.ssh/id_rsa centos@ec2-34-220-26-211.us-west-2.compute.amazonaws.com:~/
    ssh -i AWS.pem centos@ec2-34-220-26-211.us-west-2.compute.amazonaws.com
    mv id_rsa ~/.ssh/
    
    # And to not type password every time do the following so github doesn't ask for passwords constantly
    eval `ssh-agent`
    ssh-add ~/.ssh/id_rsa
    git clone git@github.com:sgnoohc/dot.git
    cd dot/
    source setup.sh
    
