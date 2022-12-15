# Terasic DE10 Agilex F-014 Acceleration Card
  ## Hardware Specification
  [DE10 Agilex card](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=115&No=1252#contents)
  ## Running oneAPI/OpenCL demo
  1.	Adding the privilege of root
  
      `sudo gedit /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf `
      
      Adding the below cmd into the line 3:
      
      `greeter-show-manual-login=true
      
      sudo passwd root`
      

2.	change the apt source to aliyun

    'lsb_release -a // got the codename of the Ubuntu version, like focal`
cd /etc/apt
sudo mv sources.list sources.list.bak  //backup the list file
gedit sources.list  //adding below to the top of the list file
sudo apt-get update  // check the new source list of the server, give the report
sudo apt-get upgrade  // upgrade the new source to local  

3.	sudo apt-get install vim

4.	install the compilation tool chain
1)	apt install g++
2)	apt install gcc
3)	apt install make
5.	install the QuartusPro-21.2.0.72-linux

6.	sudo apt install libncurses5

7.	env setting
vim ~./bashrc //adding below into the end of the file

export QUARTUS_ROOTDIR=/opt/intelFPGA_pro/21.2/quartus
export INTELFPGAOCLSDKROOT=/opt/intelFPGA_pro/21.2/hld
export AOCL_BOARD_PACKAGE_ROOT=/opt/intelFPGA_pro/21.2/hld/board/de10_agilex
export PATH=$PATH:$QUARTUS_ROOTDIR/bin:$INTELFPGAOCLSDKROOT/linux64/bin:$INTELFPGAOCLSDKROOT/bin:$INTELFPGAOCLSDKROOT/host/linux64/bin:/opt/intelFPGA_pro/21.2/qsys/bin
export LD_LIBRARY_PATH=$AOCL_BOARD_PACKAGE_ROOT/linux64/lib:$INTELFPGAOCLSDKROOT/host/linux64/lib:$AOCL_BOARD_PACKAGE_ROOT/tests/extlibs/lib
export ACL_PCIE_USE_JTAG_PROGRAMMING=1
export QUARTUS_64BIT=1

8.	unzip BSP package
password: YcgZXcEAEfVEnMe2DXUaYHupDhUWcSNaD835dAXuZYTScvCpsmVuAavKvp3ZuzuW
cp de10_agilex /opt/intelFPGA_pro/21.2/hld/board/

9.	programming the bringup sof file
cd /opt/intelFPGA_pro/21.2/hld/board/de10_agilex/bringup/B2E2_8GBx4/
sh test.sh

10.	reboot the host, test the PCIe interface
lspci | grep acce
01:00.0 Processing accelerators: Altera Corporation Device 35b4 (rev 01)

11.	if the OS is Ubuntu 18.04.6 LTS (Bionic Beaver) 
https://blog.csdn.net/wss794/article/details/127275448
install the GLIBC2.29 package

12.	install the driver 
cd  /opt/intelFPGA_pro/21.2/hld/board/de10_agilex/linux64/libexec
chmod +x *
aocl install
aocl diagnose

13.	compile the OpenCL demo
cd /opt/intelFPGA_pro/21.2/hld/board/de10_agilex/tests/vectrot_add
aoc device/vector_add.cl -o bin/vector_add.aocx -board=B2E2_8GBx4 -v
aoc device/hello_world.cl -o bin/hello_world.aocx -board=B2E2_8GBx4 -v

14.	run the vector addition demo
cd /opt/intelFPGA_pro/21.2/hld/board/de10_agilex/tests/vectrot_add/bin
./host
