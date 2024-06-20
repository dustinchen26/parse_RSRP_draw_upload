# Parse_RSRP_draw

online tool => https://dustinchen26.github.io/parse_RSRP_draw_upload

## Example
```
【How to use】
step0. Set the UE time correctly. ex:
date -s "2024-03-12 10:22:10"
step1. MobaXterm Session -> SSH -> Termnial settings -> Select "Log terminal output to": _DesktopDir_
step2. ssh into CPE. ex: 10.205.164.10
step3-1 【ATOP_CPE】use below command to read at+bnrinfo: read every 60 sec, until 3600 sec
start_time=$(date +%s); while [ $(( $(date +%s) - start_time )) -lt 3600 ]; do echo -ne "$(date) - "; echo -ne "at+bnrinfo\r\n" | microcom -t 1000 /dev/ttyUSB1 | grep -E "dBm|bnrinfo"; sleep 60; done
step3-2 【Mifi】use below command to run 10 times
for i in $(seq 1 10); do echo "$(date) - at+bnrinfo"; atcli at+bnrinfo; done
step4. paste the _DesktopDir_ output file content below to parse
	
              █████╗ ████████╗ ██████╗ ██████╗
             ██╔══██╗╚══██╔══╝██╔═══██╗██╔══██╗
             ███████║   ██║   ██║   ██║██████╔╝
             ██╔══██║   ██║   ██║   ██║██╔═══╝
             ██║  ██║   ██║   ╚██████╔╝██║
             ╚═╝  ╚═╝   ╚═╝    ╚═════╝ ╚═╝
 ---------------------------------------------------------------
   For those about to rock... (Chaos Calmer, 30c9958)
 ---------------------------------------------------------------
root@AtopTechnologies:~# while true; do output="$(date) - $(echo -ne 'at+bnrinfo\r\n' | microcom -t 1000 /dev/ttyUSB1 | grep -E 'dBm|bnrinfo')"; echo -ne "$output\n" | tee -a 10.205.164.10.txt
Tue Jan 16 11:44:36 CST 2024 - at+bnrinfo
physical cell ID:1, averaged PUSCH TX power :-255 dBm, averaged PUCCH TX power :-255 dBm,
RSRQ -11 dB, RSRP -73 dBm,SINR 34 dB
RX0 power: -62 dBm,ecio: -10 dB, rsrp: -72 dBm, phase: 0 degree, sinr: 34 dB
RX1 power: -67 dBm,ecio: -10 dB, rsrp: -77 dBm, phase: 0 degree, sinr: 32 dB
RX2 power: -60 dBm,ecio: -10 dB, rsrp: -70 dBm, phase: 0 degree, sinr: 34 dB
RX3 power: -66 dBm,ecio: -10 dB, rsrp: -76 dBm,phase: 0 degree,sinr: 33 dB

【Output】
Time	PUSCH TX power	RSRP	SINR	RX0_rsrp	RX1_rsrp	RX2_rsrp	RX3_rsrp
Tue Jan 16 11:44:36 CST 2024	-255 dBm	-73 dBm	34 dB	-72 dBm	-77 dBm	-70 dBm	-76 dBm

```
