# honeypots
python 3.8.10 updated version of gridpot

## Gridpot 
### A. GRIDPOT SETUP
This appendix summarizes the steps required to install GridPot. We changed our
virtual-machine network setting to use NAT during this setup.
1. Installing dependencies (from the command line)
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install autoconf (this includes automake)
$ sudo apt-get install libtool subversion python-dev mysql-server
$ sudo apt-get install libmysqlclient-dev libmysqld-dev
$ sudo apt-get install libxerces-c-dev python-mysqldb python-pip
$ sudo apt-get install libcurl3 libcurl4-openssl-dev libcurl4-
gnutls-dev
$ pip install –U sphinx
$ sudo apt-get install python3-sphinx libxml2-dev libxslt1-dev
$ sudo pip install lxml gevent python-dateutil mixbox
$ sudo pip install pyasn1 pycryptodomex pysmi
$ sudo apt-get install doxygen
$ sudo apt-get install libcppunit-dev libcppunit-doc
$ sudo apt-get install libncurses5-dev libncursesw5-dev
2. Pulling GridPot from GitHub
$ sudo apt install git
$ git clone https://github.com/praveen-emsec/honeypots/gridpot.git
3. Setup Conpot
$ cd gridpot/conpot/
$ conpot/ sudo make clean (if rebuilding)
$ conpot/ sudo python setup.py install
4. Setup GridLAB-D
$ cd ../gridlab-d/
$ git submodule update --init
$ mkdir build && cd build
$ make
$ sudo make install
5. Setup libiec61850
$ cd ../libiec61850
$ make
$ sudo make INSTALL_PREFIX=/usr/local install

### B. RUNNING GRIDPOT
This appendix summarizes the steps required to clear and enable logging from both
the honeypot and modeling layers, enable packet captures, and run GridPot.
0. Save & clear Conpot log
$ cat conpot.log >> conpot_original.log
$ vim conpot.log
:0 (to go to beginning of file)
dG (to erase file)
shift+zz (to save & exit)
1. Start Wireshark
$ sudo wireshark
2. Start GridLAB-D model with output to screen and file
$ cd gridpot/gridlab-d/models
$ gridlabd -D run_realtime=1 --server --debug --verbose
IEEE_13_Node_With_Houses.glm 2>&1 | tee HousesOutput.txt
3. Start Conpot using GridPot template
$ cd /gridpot/conpot/conpot/templates
$ sudo conpot -t gridpot –v
