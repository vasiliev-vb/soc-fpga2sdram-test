# soc-fpga2sdram-test
Testing FPGA2SDRAM interface on Altera Cyclone V SoC.

[Article link](https://habr.com/en/company/metrotek/blog/248145/)

## driver usage

```sh
# insmod etn.ko size=4194304 
# dd if=/dev/etn-ctrl of=/dev/null bs=1 count=1
# dd if=/dev/etn-data of=data_read bs=4M count=1
```
