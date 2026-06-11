PE1#show ip ospf neighbor

Neighbor ID     Pri   State           Dead Time   Address         Interface
4.4.4.4           1   FULL/DR         00:00:30    10.1.1.6        FastEthernet1/0
3.3.3.3           1   FULL/DR         00:00:38    10.1.1.2        FastEthernet0/0
172.16.21.21      1   FULL/BDR        00:00:32    192.168.1.6     FastEthernet3/0
11.11.11.11       1   FULL/BDR        00:00:34    192.168.1.2     FastEthernet2/0
PE1#show mpls ldp neighbor
    Peer LDP Ident: 3.3.3.3:0; Local LDP Ident 1.1.1.1:0
        TCP connection: 3.3.3.3.54665 - 1.1.1.1.646
        State: Oper; Msgs sent/rcvd: 34/35; Downstream
        Up time: 00:20:11
        LDP discovery sources:
          FastEthernet0/0, Src IP addr: 10.1.1.2
        Addresses bound to peer LDP Ident:
          10.1.1.2        3.3.3.3         10.1.1.14       10.1.1.21
    Peer LDP Ident: 4.4.4.4:0; Local LDP Ident 1.1.1.1:0
        TCP connection: 4.4.4.4.23565 - 1.1.1.1.646
        State: Oper; Msgs sent/rcvd: 34/35; Downstream
        Up time: 00:20:11
        LDP discovery sources:
          FastEthernet1/0, Src IP addr: 10.1.1.6
        Addresses bound to peer LDP Ident:
          10.1.1.6        4.4.4.4         10.1.1.10       10.1.1.22
PE1#show mpls forwarding-table
Local      Outgoing   Prefix           Bytes Label   Outgoing   Next Hop
Label      Label      or Tunnel Id     Switched      interface
17         Pop Label  4.4.4.4/32       0             Fa1/0      10.1.1.6
18         Pop Label  3.3.3.3/32       0             Fa0/0      10.1.1.2
19         23         2.2.2.2/32       0             Fa0/0      10.1.1.2
           23         2.2.2.2/32       0             Fa1/0      10.1.1.6
20         Pop Label  10.1.1.8/30      0             Fa1/0      10.1.1.6
21         Pop Label  10.1.1.12/30     0             Fa0/0      10.1.1.2
22         Pop Label  10.1.1.20/30     0             Fa0/0      10.1.1.2
           Pop Label  10.1.1.20/30     0             Fa1/0      10.1.1.6
23         No Label   172.16.10.0/24[V]   \
                                       0             Fa2/0      192.168.1.2
24         No Label   172.16.11.11/32[V]   \
                                       0             Fa2/0      192.168.1.2
25         No Label   172.16.15.0/24[V]   \
                                       0             Fa2/0      192.168.1.2
26         No Label   172.16.20.0/24[V]   \
                                       8611          Fa2/0      192.168.1.2
27         No Label   172.16.21.21/32[V]   \
                                       0             Fa3/0      192.168.1.6
28         No Label   192.168.1.0/30[V]   \
                                       6672          aggregate/VPN_SSIR
29         No Label   192.168.1.4/30[V]   \
                                       6672          aggregate/VPN_SSIR
30         No Label   192.168.1.44/30[V]   \
                                       0             Fa2/0      192.168.1.2
31         No Label   192.168.11.0/30[V]   \
                                       0             Fa2/0      192.168.1.2
32         No Label   192.168.21.0/30[V]   \
                                       0             Fa2/0      192.168.1.2
PE1#
PE1#
PE1#
PE1#
PE1#show bgp vpnv4 unicast all summary
BGP router identifier 1.1.1.1, local AS number 100
BGP table version is 19, main routing table version 19
18 network entries using 2592 bytes of memory
18 path entries using 936 bytes of memory
9/9 BGP path/bestpath attribute entries using 1188 bytes of memory
3 BGP extended community entries using 560 bytes of memory
0 BGP route-map cache entries using 0 bytes of memory
0 BGP filter-list cache entries using 0 bytes of memory
BGP using 5276 total bytes of memory
BGP activity 18/0 prefixes, 18/0 paths, scan interval 60 secs

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
2.2.2.2         4          100      29      29       19    0    0 00:20:17        4
PE1#show ip route vrf VPN_SSIR

Routing Table: VPN_SSIR
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, + - replicated route

Gateway of last resort is not set

      172.16.0.0/16 is variably subnetted, 7 subnets, 2 masks
O        172.16.10.0/24 [110/3] via 192.168.1.2, 00:20:20, FastEthernet2/0
O        172.16.11.11/32 [110/2] via 192.168.1.2, 00:20:30, FastEthernet2/0
B        172.16.12.12/32 [200/2] via 2.2.2.2, 00:19:19
O        172.16.15.0/24 [110/3] via 192.168.1.2, 00:20:20, FastEthernet2/0
O        172.16.20.0/24 [110/3] via 192.168.1.2, 00:19:56, FastEthernet2/0
O        172.16.21.21/32 [110/2] via 192.168.1.6, 00:20:30, FastEthernet3/0
B        172.16.22.22/32 [200/2] via 2.2.2.2, 00:19:19
      192.168.1.0/24 is variably subnetted, 7 subnets, 2 masks
C        192.168.1.0/30 is directly connected, FastEthernet2/0
L        192.168.1.1/32 is directly connected, FastEthernet2/0
C        192.168.1.4/30 is directly connected, FastEthernet3/0
L        192.168.1.5/32 is directly connected, FastEthernet3/0
B        192.168.1.8/30 [200/0] via 2.2.2.2, 00:19:21
B        192.168.1.12/30 [200/0] via 2.2.2.2, 00:19:21
O        192.168.1.44/30 [110/3002] via 192.168.1.2, 00:19:48, FastEthernet2/0
      192.168.11.0/30 is subnetted, 1 subnets
O        192.168.11.0 [110/2] via 192.168.1.2, 00:20:32, FastEthernet2/0
      192.168.21.0/30 is subnetted, 1 subnets
O        192.168.21.0 [110/13] via 192.168.1.2, 00:19:49, FastEthernet2/0




CE11#ping 12.12.12.12
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 12.12.12.12, timeout is 2 seconds:
!!!!!


CE11#ping 22.22.22.22
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 22.22.22.22, timeout is 2 seconds:
!!!!!







Federateur1#show standby brief
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State   Active          Standby         Virtual IP
Vl10        10   110 P Active  local           172.16.10.3     172.16.10.1
Vl15        15   110 P Active  local           172.16.15.3     172.16.15.1
Vl20        20   110 P Active  local           172.16.20.3     172.16.20.1


Federateur1#show etherchannel summary
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      f - failed to allocate aggregator

        M - not in use, minimum links not met
        u - unsuitable for bundling
        w - waiting to be aggregated
        d - default port


Number of channel-groups in use: 1
Number of aggregators:           1

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Et0/2(P)





Federateur2#show standby brief
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State   Active          Standby         Virtual IP
Vl10        10   100   Standby 172.16.10.2     local           172.16.10.1
Vl15        15   100   Standby 172.16.15.2     local           172.16.15.1
Vl20        20   100   Standby 172.16.20.2     local           172.16.20.1








CE-Branch1#show ip sla statistics 11
IPSLAs Latest Operation Statistics

IPSLA operation id: 11
Type of operation: udp-jitter
        Latest RTT: 118 milliseconds
Latest operation start time: *13:04:26.551 UTC Thu Jun 11 2026
Latest operation return code: OK
RTT Values:
        Number Of RTT: 10               RTT Min/Avg/Max: 104/118/148 milliseconds
Latency one-way time:
        Number of Latency one-way Samples: 0
        Source to Destination Latency one way Min/Avg/Max: 0/0/0 milliseconds
        Destination to Source Latency one way Min/Avg/Max: 0/0/0 milliseconds
Jitter Time:
        Number of SD Jitter Samples: 9
        Number of DS Jitter Samples: 8
        Source to Destination Jitter Min/Avg/Max: 0/14/44 milliseconds
        Destination to Source Jitter Min/Avg/Max: 0/9/27 milliseconds
Packet Loss Values:
        Loss Source to Destination: 0           Loss Destination to Source: 0
        Out Of Sequence: 0      Tail Drop: 0
        Packet Late Arrival: 0  Packet Skipped: 0
Voice Score Values:
        Calculated Planning Impairment Factor (ICPIF): 0
        Mean Opinion Score (MOS): 0
Number of successes: 7
Number of failures: 1
Operation time to live: Forever


















