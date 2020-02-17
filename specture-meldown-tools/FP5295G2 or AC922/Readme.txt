#查询系统CPU漏洞补丁情况：
grep -r . /sys/devices/system/cpu/vulnerabilities
## 输出形如：
#/sys/devices/system/cpu/vulnerabilities/spectre_v2:Mitigation: Indirect branch serialisation (kernel only)
#/sys/devices/system/cpu/vulnerabilities/spec_store_bypass:Mitigation: Kernel entry/exit barrier (eieio)
#/sys/devices/system/cpu/vulnerabilities/spectre_v1:Mitigation: __user pointer sanitization, ori31 speculation barrier enabled
#/sys/devices/system/cpu/vulnerabilities/meltdown:Mitigation: RFI Flush, L1D private per thread

#登录到BMC并打上补丁
sshpass -p 0penBmc ssh -l root $BMC_IP 'cat > /var/lib/obmc/cfam_overrides' <<- EOF
 Control speculative execution mode
 Init level 0 — Kernel and User protection (safest, default)
Init level 1 — Kernel protection only
Init level 2 — No protection
0 0x283a 0x00000002  # bits 28:31 are used for init level -- in this case 2
0 0x283F 0x20000000  # Indicate scratch 3 is valid
EOF

#断电继而加电启动

#重新查询系统CPU漏洞补丁情况：
grep -r . /sys/devices/system/cpu/vulnerabilities
/sys/devices/system/cpu/vulnerabilities/spectre_v2:Vulnerable
/sys/devices/system/cpu/vulnerabilities/spec_store_bypass:Not affected
/sys/devices/system/cpu/vulnerabilities/spectre_v1:Not affected
/sys/devices/system/cpu/vulnerabilities/meltdown:Not affected




