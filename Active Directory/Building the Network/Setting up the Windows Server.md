# Setting up the Windows Server for the virtual network

In this section of the knowledge base I am going to be installing **Windows 2019 2022**. Using the **Network Plan** I am going to build the network with the computers requirements. 

## Setup

The hypervisor I am going to use is a type 2, and I am going to use a program called **Boxes** to manage the VMs in a simple interface. FIrst I am going to click the **"+"** button on the top left of the screen and click on the option **"Install from File"**.

![](https://thatdigitalguy.github.io/knowledge-base/Media/Active%20Directory/serv-setup/boxes-install-file.png)

Next I am going to navigate to where the VM images are stored and select the Windows Server 2019 iso file.

![](https://thatdigitalguy.github.io/knowledge-base/Media/Active%20Directory/serv-setup/boxes-install-from-file.png)

After that screen the configuration for the VM pop up and I will name the VM, **"SRV01-AD"**. After confirming all the settings I am going to click the **"Create"** button on the dialog window.

![](/home/rhysm/.config/marktext/images/2024-02-28-08-25-11-image.png)ectory/serv-setup/boxes-SRV01-configuration.png)

Once I click **"Create"**, Boxes will automatically create, start, and connect to the VM. When the **VM loads**, then I will go through the setup of Windows Server 2019. First, I will select my **language, time, and keyboard settings**.



![](https://thatdigitalguy.github.io/knowledge-base/Media/Active%20Directory/serv-setup/SRV01-setup-lang.png)



After this screen I clicked the **"Install button"**. After that I am going to choose the version of **Windows Server 2019**, which the verision I am going to use is the **Datacenter** version with the Desktop Experience. Then click **next**.



![](https://thatdigitalguy.github.io/knowledge-base/Media/Active%20Directory/serv-setup/SRV01-setup-version.png)



Next, the setup will ask what type of installation you want. The option I am going to pick is **Custom: Install Windows Only** then click next.



![](https://thatdigitalguy.github.io/knowledge-base/Media/Active%20Directory/serv-setup/SRV01-setup-install-type.png)



Next part is the disk partioning, on this page I am going to check the settings and click next. Then Windows will start to install.



![](/home/rhysm/Documents/knowledge-base/Media/Active%20Directory/serv-setup/SRV01-setup-disks.png)



![](/home/rhysm/Documents/knowledge-base/Media/Active%20Directory/serv-setup/SRV01-setup-installing.png)



## Setting up the Administrator User



I forgot to screenshot the setup for the Administrator account, however it asks for you to add a password to it. After that you can log in to the Windows Server.



![](/home/rhysm/Documents/knowledge-base/Media/Active%20Directory/serv-setup/SRV01-system-login.png)
