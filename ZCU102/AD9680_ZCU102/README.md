# AD9680-ZCU102 Data Capturing system
(Petalinux,Vivado v2023.2)
Firstly, this design has been heavily influenced by the reference link: https://wiki.analog.com/resources/eval/user-guides/ad9695_fmc
but for ad9680 which has pin compatiblity with ad9695

Steps to follow:
1-)
	download reference ZCU projects from https://github.com/analogdevicesinc/hdl
2-)
	under ADI_git_repo_path/hdl/projects/ copy folder ./AD9680_PETALINUX/VIVADO/ad9680_fmc/
	├─ projects
	│    ├ ad6676evb
	│    ├ ad9467_fmc
	│    ├ ad9680_fmc (***new one***)
	│    ·
	│    ├ common
	│    ├ fmcomms2
	│    │   ├ ac701
	│    │   ├ common
	│    │   ├ kc705
	│    │   ·
	│    │   ├ zed
	│    │   └ Makefile
	│    ├ adrv9009
	│    ├ scripts
	│    ·
	│    └ Makefile
	└─ library
	·
	└─ README.md
	
3-)
	go inside this folder any simply run make (assuming required dependencies are already installed)
	after this make command it will build the project from script (it is highly recommended to inspect this design) some part 
	of it is given below.
	!(./images/block_design.png)

4-)
	after this step it is possible to use kuiper linux I believe, but as almost any block people who share IP also share their drivers (kind of
	imagine as SDK, so ADI also share this drivers as yocto layers to be used in custom OS projects which is in our case petalinux)
	yocto layer is shared at : https://github.com/analogdevicesinc/meta-adi/tree/main/meta-adi-xilinx   
	at this link they also share how to add this yocto layer to petalinux.
	
5-) 	
	by inspecting above link if someone doesn't want to write these delete nodes etc. its prepared version is added to ./AD9680_PETALINUX/DEVICE-TREE/ 

6-)
	under ADI_git_repo_path/hdl/projects/ad9680_fmc/zcu102/ad9680_zcu102.sdk/meta-adi/meta-adi-xilinx/recipes-bsp/device-tree/
	add ./AD9680_PETALINUX/DEVICE-TREE/* 
	
7-)	
	Some details can be enabled in peta-linux to ease further iio-oscilloscope usage.​
	!(./images/petalinux_config.png)
	Static ip is assigned to ZCU102 because iio-oscilloscope use ethernet connection to take from
	ZCU102 to host​

	Setting can be adjust at petalinux-config menu's ​

	Subsystem AUTO Hardware Settings->Ethernet Settings 
8-)
	build the project
9-)
	Clock source configuration is provided by first steps link, same channels are used but frequencies are changed a little.
	!(./images/clock_source_config.png)
10-)
	system connection:
	!(./images/system.png)
11-)
	kick the system (I used SDcard booting) you should see iio devices as below:
	!(./images/iio_check.png)
12-)
	iio-oscilloscope application should also see the device at 192.168.2.1 (assuming you are using private ip etc, but should be checked)
	!(./images/iio_oscilloscope.png)
13-)
	result:
	!(./images/result.png)
	
