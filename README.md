Tested on
------------------------------------------
Teltonika Rut240 /SLM750 module/ firmware version: RUT2XX_R_00.01.14.7
Windows 11 25H2


Used software
----------------------------------------
Putty SSH (https://putty.org/index.html)
WinSCP	  (https://winscp.net/eng/download.php)
USR-VCOM  (https://www.waveshare.com/wiki/File:USR-VCOM_V3.7.1.520.7z)
socat     (https://github.com/darkerego/mips-binaries/raw/master/socat)
QPST	  (https://qpsttool.com/qpst-tool-v2-7-496/)


Guide
---------------------------------------
1) Connect to your router via SSH and log in
2) Upload socat to router /tmp via SCP
3) Run **chmod +x /tmp/socat**
4) Run **/tmp/socat tcp-l:9000,reuseaddr,fork file:/dev/ttyUSB0,nonblock,raw,echo=0**
> Your debugging tty might be different, try: /ttyUSB1 /ttyUSB2 or /ttyUSB3
5) Open *USR-VCOM* and click **Add COM**
6) Select non-used Virtual COM (you can see used in Device Manager)
7) **Net Protocol: TCP Client | Remote IP/addr: RouterIP | Port: 9000**
8) Open *QPST* configration
9) **Ports -> Add New Port -> Your created virtual port from USR-VCOM**
10) After a few seconds the column **Phone** should not be empty.
> If it says No Phone, then you messed up somewhere or you don't use debugging ttyUSB
11) You should create backup in case something mess up: **Start Clients -> Software Download -> Backup -> Browse** (destination of save file) **-> Start**
12) **Start Clients -> Service Programming -> OK**
13) **Read from Phone** (service code 000000, 012345 or 123456)
14) Find **NAS** in top menu
15) Fill in the **IMEI** (you don't put in last digit, **select Luhn check digit**)
16) **Write to Phone**
17) Wait for it to completely finish and close everything. 
18) Unplug router power cord and wait 15 seconds
19) Connect back via SSH and check gsmctl -i
