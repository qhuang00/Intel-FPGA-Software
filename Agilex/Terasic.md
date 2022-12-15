# Terasic DE10 Agilex F-014 Acceleration Card
## Server info
192.168.1.xx
## Hardware Specification
  [DE10 Agilex card](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=115&No=1252#contents)
## Verify oneAPI/OpenCL installation
  ```shell
  cd  /opt/intelFPGA_pro/21.2/hld/board/de10_agilex/linux64/libexec
  chmod +x *
  aocl install
  aocl diagnose
```
## Compile the OpenCL demo
```shell
cd /opt/intelFPGA_pro/21.2/hld/board/de10_agilex/tests/vectrot_add
aoc device/vector_add.cl -o bin/vector_add.aocx -board=B2E2_8GBx4 -v
aoc device/hello_world.cl -o bin/hello_world.aocx -board=B2E2_8GBx4 -v
```
##	Run the vector addition demo
```shell
cd /opt/intelFPGA_pro/21.2/hld/board/de10_agilex/tests/vectrot_add/bin
./host
```
