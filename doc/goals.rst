Project Goals
=============

-----------------------------------------------------------------------------
*GOAL-1:* *Develop Packet Sniffer application using Python*
-----------------------------------------------------------------------------
^^^^^^^^^^^^^^^^
Original Goal
^^^^^^^^^^^^^^^^
This goal will be achieved by researching and identifying an open source Python library, that will help to capture all the network packets at any particular network interface. These packets are then decoded and studies in details to analyze the behaviors of network communication at different levels.

^^^^^^^^^^^^^^^^^^^^^^
How did I achieve it?
^^^^^^^^^^^^^^^^^^^^^^

    Yes, I achieved this goal. As suggested by instructor, I have used *pycap* library to capture packets. User Level wrapper has been developed in python. Usage and CLI arguments are provided in this documentation. As this part of the project was relatively unimportant, and completely unrelated to other two goals of my project, I spent limited amount of time to develop this Packet Sniffing application.

------------------------------------------------------------------------------------
*GOAL-2:* *Identify and study the SNMP interface with Airport Extreme Router.*
------------------------------------------------------------------------------------
^^^^^^^^^^^^^^^^
Original Goal
^^^^^^^^^^^^^^^^

    Researching and gaining a level of understanding of the SNMP protocol and the configuration management concepts will achieve this goal.  A proper link with Apple Airport routers via NetSNMP will be established, and various Oid supported by Airport MiB will be identified. A Python code also will be developed to query these devices and fetch the data related to network usage monitoring.

^^^^^^^^^^^^^^^^^^^^^^
How did I achieve it?
^^^^^^^^^^^^^^^^^^^^^^

    Yes, I achieved this goal. I have developed Object Oriented SNMP wrapper, and researched MiB standard specifications for Apple's Airport class routers. Information related to Apple's Airport Extreme Mib can be found on: *http://support.apple.com/kb/DL1186*. I was able to connect to Airport Extreme and Express routers at home, to query various network parameters via netsnmp.

--------------------------------------------------------------------------------
*GOAL-3:*  *Obtain data and feed it to the network monitoring/graphing tool*
--------------------------------------------------------------------------------

^^^^^^^^^^^^^^^^
Original Goal
^^^^^^^^^^^^^^^^

    This goal will be achieved once the lower level python code is established for fetching the data from router. At this stage, this data will be presented using some Python graphing libraries or any logging/monitoring tool. If monitoring tool is used, then there will be some interfacing mechanism (‘plugin’) developed on top of previous code in Python. This data also gives an understanding and wide overview of actual network behavior and traffic statistics, which is very much insightful, as an ECE student with very less background of networking.

^^^^^^^^^^^^^^^^^^^^^^
How did I achieve it?
^^^^^^^^^^^^^^^^^^^^^^

    Yes, this goal was achieved. I used *Munin Monitoring tool* to generate graphs from the parameters provided by SNMP wrapper (via python plugin scripts). Airport_Network_Monitor uses Munin (munin-monitoring.org/) tool generate graphs and monitor other parameneters related to Apple's Airport Express/Extreme or Time Capsule Devices. The project basically consist of:

 | 1) Top Level SNMP wrapper for Airport Extreme (Airport_Monitor.py)
 | 2) Several Munin plugins (written in Python) to feed the data and other graph related configuration information to Munin Plugin.

   For example, 'Airport_Wireless_Clients.py' is plugin script, used to feed data (and graph configuration) to Munin, for monitoring no. of clients connected to Airport Router. There are several Plugin Scripts in the Folder *Airport_Monitor*:

    | - Airport_Client_Error_Packets.py
    | - Airport_Client_Traffic.py
    | - Airport_Client_Signal_Strength.py
    | - Airport_Client_Noise.py
    | - Airport_DHCP_Clients.py
    | - Airport_Wireless_Clients.py
    | - Airport_Client_Rate.py 
    | - Airport_WAN_Traffic.py  

All these scripts use Airport_Monitor.py to fetch SNMP data from the router, and supply this data to munin.
Munin automatically generates graph for these scripts, if they are placed in */etc/munin/plugins* folder.

Graphs generated by Munin can be shown by Local Web Server (Apache2 or lighthttpd).
