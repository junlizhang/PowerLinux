Description:
 Enable/Disable OpenPOWER Specture/Meldown patch.
 适用机型: OpenPOWER机器,如FP5280G2、FP5290G2
操作说明:
1.开机进入OS (REHL or Ubuntu LE),进入本文件夹

2.Enable Specture/Meldown Patch 命令如下: (高安全，低性能)
./pflash -e -f -p attrOverride_default_enable_meldown_patch.bin -P ATTR_TMP
重启系统后生效.
Note: 需要做完整的重新IPL的过程(系统power down 再 power on)。
      在OS下执行"reboot"，会使系统做fast reboot，该reboot不会跑Hostboot，所以不是完整的IPL。

3.Disable Specture/Meldown Patch，命令如下: (低安全，高性能)
./pflash -e -f -p attrOverride_disable_meldown_patch.bin -P ATTR_TMP
重启系统后生效。
Note: 需要做完整的重新IPL的过程(系统power down 再 power on)。
      在OS下执行"reboot"，会使系统做fast reboot，该reboot不会跑Hostboot，所以不是完整的IPL。
