# LinuxShell_route


* 查詢路由設定

usage

      route [args] cmd [[modifiers] args]
      
內部指令的使用情境

    route add -net 192.56.76.0 netmask 255.255.255.0 dev eth0
    
    route add -net 10.10.10.0 netmask 255.255.255.0 gw 10.10.10.1
    // 設定經由 10.10.10.0 網段的流量經由 10.10.10.1 進行傳送。
    
    route add -host 192.168.10.10 dev eth0
    // 設定要往目的地主機的流量經由網卡/介面 eth0 傳送。
    
    route change 10.10.195.251/32 10.10.195.10
    // 將 10.10.195.251/32 網段流量的 gw 改成 10.10.195.10。
    
 * args
 
    * a all, 顯示所有連接中的 socket。
    
    * c continues, 持續列出網路狀態。
     
    * C Cache, 顯示路由的快取資訊。
    
    * F, Forward Info, 顯示轉發的基本資訊。
    
    * g, group, 顯示 Multicast 群組名稱。
     
    * I, Interface, 顯示網路介面資訊的表單。
    
    * l, list, 顯示監控中伺服器的 Socket。
    
    * n, name no, 直接使用 IP addr, 不使用名稱。
    
    * o, ouptput counter, 顯示計時器。
     
    * p, pid, 顯示計時器。
    
    * r, routing tale, 顯示路由表。
    
    * s, statistics, 顯示網路資訊統計表。
     
    * t, tcp, 顯示 TCP 連線狀況。
    
    * u, ucp, 顯示 UCP 連線狀況。
    
    * w, 顯示 RAW 連線狀況。
    
    * x, 列出 Unix 傳輸協定連線中的相關位址。
    
 
* cmd

    * add: 增加路由紀錄。
    
    * del: 刪除路由紀錄。
    
    * -net: 指定網段位址。
    
    * -host: 指定主機位址。
    
    * target: 目的地位址：
      

* the arg for cmd

   * frequently usage

          +---------------+-----------------------------+
          | dev + [IF]    | 指定路由僅跟特定裝置。          |
          +---------------+-----------------------------+
          | gw + [IP addr]| 閘道網路位址。                |
          +---------------+-----------------------------+
          | netmask + [NM]| 網段的子網路遮罩。             |
          +---------------+-----------------------------+

    * other usage
    
          +---------------+---------------------------------------+
          | mss + [M]     | max seg size, 設定 TCP 傳輸最大區塊長度。 |
          +---------------+---------------------------------------+
          | reject        | 指定拒絕的路由。                         |
          +---------------+---------------------------------------+
          | metric + [M]  | metric field, 指定路由表中的欄位長度      |
          +---------------+---------------------------------------+
    

# Unix Bash Alternative

    netstat 

      ✗ netstat
      Active Internet connections
      Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)    
      tcp4       0      0  192.168.100.24.50346   tsa01s07-in-f10..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50345   tsa01s07-in-f10..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50344   nrt13s51-in-f14..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50343   tsa03s06-in-f10..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50342   nrt13s51-in-f14..https ESTABLISHED


    ✗ netstat -nr
    
      Routing tables

      Internet:
      Destination        Gateway            Flags        Netif Expire
      
      default            192.168.100.1      UGSc           en0 
      
      127.0.0.1          127.0.0.1          UH             lo0       
      
      192.168.100        link#4             UCS            en0      !
      192.168.100.1/32   link#4             UCS            en0      !
      
      192.168.100.1      0:9:f:b9:4c:59     UHLWIir        en0   1177
      
      192.168.100.3      f0:99:b6:31:7:d5   UHLWI          en0     83
      192.168.100.13     1c:91:48:9d:49:c8  UHLWIi         en0   1012      
      192.168.100.24/32  link#4             UCS            en0      !
      
      192.168.100.255    ff:ff:ff:ff:ff:ff  UHLWbI         en0      !
      
      224.0.0/4          link#4             UmCS           en0      !
      224.0.0.251        1:0:5e:0:0:fe      UHmLWI         en0       
      
      255.255.255.255/32 link#4             UCS            en0      !


* args for netsat

      ✗ netstat -o
      Usage:	
            netstat [-AaLlnW] [-f address_family | -p protocol]
            netstat [-gilns] [-f address_family]
            netstat -i | -I interface [-w wait] [-abdgRtS]
            netstat -s [-s] [-f address_family | -p protocol] [-w wait]
            netstat -i | -I interface -s [-f address_family | -p protocol]
            netstat -m [-m]
            netstat -r [-Aaln] [-f address_family]
            netstat -rs [-s]


(1) netstat -m

      ✗ netstat -m
      
      484/1238 mbufs in use:
            244 mbufs allocated to data
            240 mbufs allocated to packet tags
            754 mbufs allocated to caches
            
      240/1004 mbuf 2KB clusters in use
      0/1096 mbuf 4KB clusters in use
      0/41 mbuf 16KB clusters in use
      7549 KB allocated to network (8.1% in use)
      0 KB returned to the system
      0 requests for memory denied
      0 requests for memory delayed
      0 calls to drain routines
      
(2) netstat -rs

      ✗ netstat -rs
      routing:
            0 bad routing redirect
            0 dynamically created route
            0 new gateway due to redirects
            13492 destinations found unreachable
            0 use of a wildcard route
            0 lookup returned indirect routes pointing to indirect gateway route
            1 route not in table but not freed

(3) netstat -s

            ✗ netstat -s
            
* tcp

            tcp:
                  0 packet sent
                        0 data packet (0 byte)
                        0 data packet (0 byte) retransmitted
                        0 resend initiated by MTU discovery
                        0 ack-only packet (0 delayed)
                        0 URG only packet
                        0 window probe packet
                        0 window update packet
                        0 control packet
                        0 data packet sent after flow control
                        0 challenge ACK sent due to unexpected SYN
                        0 challenge ACK sent due to unexpected RST
                        0 checksummed in software
                              0 segment (0 byte) over IPv4
                              0 segment (0 byte) over IPv6
                  0 packet received
                        0 ack (for 0 byte)
                        0 duplicate ack
                        0 ack for unsent data
                        0 packet (0 byte) received in-sequence
                        0 completely duplicate packet (0 byte)
                        0 old duplicate packet
                        0 received packet dropped due to low memory
                        0 packet with some dup. data (0 byte duped)
                        0 out-of-order packet (0 byte)
                        0 packet (0 byte) of data after window
                        0 window probe
                        0 window update packet
                        0 packet recovered after loss
                        0 packet received after close
                        0 bad reset
                        0 discarded for bad checksum
                        0 checksummed in software
                              0 segment (0 byte) over IPv4
                              0 segment (0 byte) over IPv6
                        0 discarded for bad header offset field
                        0 discarded because packet too short
                  0 connection request
                  0 connection accept
                  0 bad connection attempt
                  0 listen queue overflow
                  0 connection established (including accepts)
                  0 connection closed (including 0 drop)
                        0 connection updated cached RTT on close
                        0 connection updated cached RTT variance on close
                        0 connection updated cached ssthresh on close
                        0 connection initialized RTT from route cache
                        0 connection initialized RTT variance from route cache
                        0 connection initialized ssthresh from route cache
                  0 embryonic connection dropped
                  0 segment updated rtt (of 0 attempt)
                  0 retransmit timeout
                        0 connection dropped by rexmit timeout
                        0 connection dropped after retransmitting FIN
                        0 unnecessary packet retransmissions
                  0 persist timeout
                        0 connection dropped by persist timeout
                  0 keepalive timeout
                        0 keepalive probe sent
                        0 connection dropped by keepalive
                        0 connection dropped by keepalive offload
                  0 correct ACK header prediction
                  0 correct data packet header prediction
                  0 SACK recovery episode
                  0 segment rexmit in SACK recovery episodes
                  0 byte rexmit in SACK recovery episodes
                  0 SACK option (SACK blocks) received
                  0 SACK option (SACK blocks) sent
                  0 SACK scoreboard overflow
                  0 LRO coalesced packet
                        0 time LRO flow table was full
                        0 collision in LRO flow table
                        0 time LRO coalesced 2 packets
                        0 time LRO coalesced 3 or 4 packets
                        0 time LRO coalesced 5 or more packets
                  0 limited transmit done
                  0 early retransmit done
                  0 time cumulative ack advanced along with SACK
                  0 probe timeout
                        0 time retransmit timeout triggered after probe
                        0 time probe packets were sent for an interface
                        0 time couldn't send probe packets for an interface
                        0 time fast recovery after tail loss
                        0 time recovered last packet 
                        0 SACK based rescue retransmit
                  0 client connection attempted to negotiate ECN
                        0 client connection successfully negotiated ECN
                        0 time graceful fallback to Non-ECN connection
                        0 time lost ECN negotiating SYN, followed by retransmission
                        0 server connection attempted to negotiate ECN
                        0 server connection successfully negotiated ECN
                        0 time lost ECN negotiating SYN-ACK, followed by retransmission
                        0 time received congestion experienced (CE) notification
                        0 time CWR was sent in response to ECE
                        0 time sent ECE notification
                        0 connection received CE atleast once
                        0 connection received ECE atleast once
                        0 connection using ECN have seen packet loss but no CE
                        0 connection using ECN have seen packet loss and CE
                        0 connection using ECN received CE but no packet loss
                        0 connection fell back to non-ECN due to SYN-loss
                        0 connection fell back to non-ECN due to reordering
                        0 connection fell back to non-ECN due to excessive CE-markings
                        0 connection fell back caused by connection drop due to RST
                        0 connection fell back due to drop after multiple retransmits 
                        0 connection fell back due to RST after SYN
                  0 time packet reordering was detected on a connection
                        0 time transmitted packets were reordered
                        0 time fast recovery was delayed to handle reordering
                        0 time retransmission was avoided by delaying recovery
                        0 retransmission not needed 
                  0 retransmission due to tail loss
                  0 time DSACK option was sent
                        0 time DSACK option was received
                        0 time DSACK was disabled on a connection
                        0 time recovered from bad retransmission using DSACK
                        0 time ignored DSACK due to ack loss
                        0 time ignored old DSACK options
                  0 time PMTU Blackhole detection, size reverted
                  0 connection were dropped after long sleep
                  0 connection had stretch ack algorithm disabled
                  0 time a TFO-cookie has been announced
                  0 SYN with data and a valid TFO-cookie have been received
                  0 SYN with TFO-cookie-request received
                  0 time an invalid TFO-cookie has been received
                  0 time we requested a TFO-cookie
                        0 time the peer announced a TFO-cookie
                  0 time we combined SYN with data and a TFO-cookie
                        0 time our SYN with data has been acknowledged
                  0 time a connection-attempt with TFO fell back to regular TCP
                  0 time a TFO-connection blackhole'd
                  0 time a TFO-cookie we sent was wrong
                  0 time did not received a TFO-cookie we asked for
                  0 time TFO got disabled due to heuristicsn
                  0 time TFO got blackholed in the sending direction
                  0 time maximum segment size was changed to default
                  0 time maximum segment size was changed to medium
                  0 time maximum segment size was changed to low
                  0 timer drift less or equal to 1 ms
                  0 timer drift less or equal to 10 ms
                  0 timer drift less or equal to 20 ms
                  0 timer drift less or equal to 50 ms
                  0 timer drift less or equal to 100 ms
                  0 timer drift less or equal to 200 ms
                  0 timer drift less or equal to 500 ms
                  0 timer drift less or equal to 1000 ms
                  0 timer drift greater than to 1000 ms
                  
* udp

            udp:
                  18821 datagrams received
                        0 with incomplete header
                        0 with bad data length field
                        0 with bad checksum
                        0 with no checksum
                        12697 checksummed in software
                              7855 datagrams (1714257 bytes) over IPv4
                              4842 datagrams (1289821 bytes) over IPv6
                        326 dropped due to no socket
                        556 broadcast/multicast datagrams undelivered
                        0 time multicast source filter matched
                        0 dropped due to full socket buffers
                        0 not for hashed pcb
                        17939 delivered
                  8580 datagrams output
                        3246 checksummed in software
                              2605 datagrams (404596 bytes) over IPv4
                              641 datagrams (150146 bytes) over IPv6
            netstat: sysctl: net.inet.ip.input_perf_data: No such file or directory
            ip:
                  268100 total packets received
                        0 bad header checksum
                        267302 headers (5352900 bytes) checksummed in software
                        0 with size smaller than minimum
                        0 with data size < data length
                        238 with data size > data length
                              0 packet forced to software checksum
                        0 with ip length > max ip packet size
                        0 with header length < data size
                        0 with data length < header length
                        0 with bad options
                        0 with incorrect version number
                        0 fragment received
                              0 dropped (dup or out of space)
                              0 dropped after timeout
                              0 reassembled ok
                        248844 packets for this host
                        688 packets for unknown/unsupported protocol
                        0 packet forwarded (0 packet fast forwarded)
                        0 packet not forwardable
                        18568 packets received for unknown multicast group
                        0 redirect sent
                        1290 input packets not chained due to collision
                        208164 input packets processed in a chain
                        403 input packets unable to chain
                        36881 input packet chains processed with length greater than 2
                        12708 input packet chains processed with length greater than 4
                        58243 input packets did not go through list processing path
                  199248 packets sent from this host
                        0 packet sent with fabricated ip header
                        0 output packet dropped due to no bufs, etc.
                        0 output packet discarded due to no route
                        0 output datagram fragmented
                        0 fragment created
                        0 datagram that can't be fragmented
                        0 tunneling packet that can't find gif
                        0 datagram with bad address in header
                        0 packet dropped due to no bufs for control data
                        0 packet dropped due to NECP policy
                        199021 headers (3980456 bytes) checksummed in software
                        
* icmp

            icmp:
                  326 calls to icmp_error
                  0 error not generated 'cuz old message was icmp
                  Output histogram:
                        destination unreachable: 326
                  0 message with bad code fields
                  0 message < minimum length
                  0 bad checksum
                  0 message with bad length
                  0 multicast echo requests ignored
                  0 multicast timestamp requests ignored
                  Input histogram:
                        destination unreachable: 224
                  0 message response generated
                  ICMP address mask responses are disabled
            igmp:
                  464 messages received
                  0 message received with too few bytes
                  0 message received with wrong TTL
                  0 message received with bad checksum
                  0 V1/V2 membership queries received
                  132 V3 membership queries received
                  0 membership queries received with invalid field(s)
                  132 general queries received
                  0 group queries received
                  0 group-source queries received
                  0 group-source queries dropped
                  332 membership reports received
                  0 membership report received with invalid field(s)
                  332 membership reports received for groups to which we belong
                  0 V3 report received without Router Alert
                  4 membership reports sent
                  
* ipsec

            ipsec:
                  0 inbound packet processed successfully
                  0 inbound packet violated process security policy
                  0 inbound packet with no SA available
                  0 invalid inbound packet
                  0 inbound packet failed due to insufficient memory
                  0 inbound packet failed getting SPI
                  0 inbound packet failed on AH replay check
                  0 inbound packet failed on ESP replay check
                  0 inbound packet considered authentic
                  0 inbound packet failed on authentication
                  0 outbound packet processed successfully
                  0 outbound packet violated process security policy
                  0 outbound packet with no SA available
                  0 invalid outbound packet
                  0 outbound packet failed due to insufficient memory
                  0 outbound packet with no route
                  
* arp

            arp:
                  70 broadast ARP requests sent
                  0 unicast ARP request sent
                  531 ARP replies sent
                  0 ARP announcement sent
                  9071 ARP requests received
                  61 ARP replies received
                  9133 total ARP packets received
                  0 ARP conflict probe sent
                  0 invalid ARP resolve request
                  0 total packet dropped due to lack of memory
                  0 total packet held awaiting ARP reply
                  0 total packet dropped due to no ARP entry
                  11 total packets dropped during ARP entry removal
                  27 ARP entries timed out
                  0 Duplicate IP seen
            mptcp:
                  0 data packet sent
                  0 data byte sent
                  0 data packet received
                  0 data byte received
                  0 packet with an invalid MPCAP option
                  0 packet with an invalid MPJOIN option
                  0 time primary subflow fell back to TCP
                  0 time secondary subflow fell back to TCP
                  0 DSS option drop
                  0 other invalid MPTCP option
                  0 time the MPTCP subflow window was reduced
                  0 bad DSS checksum
                  0 time received out of order data 
                  0 subflow switch
                  0 subflow switch due to advisory
                  0 subflow switch due to rtt
                  0 subflow switch due to rto
                  0 subflow switch due to peer
                  0 number of subflow probe
            ip6:
                  16743 total packets received
                        0 with size smaller than minimum
                        0 with data size < data length
                        0 with data size > data length
                              0 packet forced to software checksum
                        0 with bad options
                        0 with incorrect version number
                        0 fragment received
                              0 dropped (dup or out of space)
                              0 dropped after timeout
                              0 exceeded limit
                              0 reassembled ok
                              0 atomic fragments received
                        10378 packets for this host
                        0 packet forwarded
                        6283 packets not forwardable
                        0 redirect sent
                        6283 multicast packets which we don't join
                        0 packet whose headers are not continuous
                        0 tunneling packet that can't find gif
                        0 packet discarded due to too may headers
                        0 forward cache hit
                        0 forward cache miss
                        0 packet dropped due to no bufs for control data
                        0 input packet dropped due to too short length 
                        0 input packet dropped due to missing CLAT46 IPv6 address
                        0 input packet dropped due to missing CLAT46 IPv4 address
                        0 input packet dropped due to CLAT46 IPv4 address 
* rip

            rip6:
                  0 message received
                  0 checksum calculation on inbound
                  0 message with bad checksum
                  0 message dropped due to no socket
                  0 multicast message dropped due to no socket
                  0 message dropped due to full socket buffers
                  0 delivered
                  0 datagram output
            pfkey:
                  0 request sent to userland
                  0 byte sent to userland
                  0 message with invalid length field
                  0 message with invalid version field
                  0 message with invalid message type field
                  0 message too short
                  0 message with memory allocation failure
                  0 message with duplicate extension
                  0 message with invalid extension type
                  0 message with invalid sa type
                  0 message with invalid address extension
                  0 request sent from userland
                  0 byte sent from userland
                  0 message toward single socket
                  0 message toward all sockets
                  0 message toward registered sockets
                  0 message with memory allocation failure
            kevt:
                  23 current kernel control sockets
                  1511 kernel control generation count
                  0 bad vendor failure
                  0 message too big failure
                  0 out of memory failure
                  0 message dropped due to full socket buffers
                  21976 messages posted
            kctl:
                  0 total kernel control module registered
                  12 current kernel control modules registered
                  44 current kernel control sockets
                  156 kernel control generation count
                  94 connection attempts
                  0 connection failure
                  3 send failures
                  0 send list failure
                  0 enqueue failure
                  0 packet dropped due to full socket buffers
                  0 failure with bad kern_ctl_ref
                  0 register failure because of too many kern_ctl_ref
                  0 enqueuedata failure because could not allocate a packet
                  0 enqueuedata failure due to full socket buffers
            xbkidle:
                  1 max per process
                  600 maximum time (seconds)
                  131072 high water mark
                  0 socket option not supported failure
                  0 too many sockets failure
                  0 total socket requested OK
                  0 extended bk idle socket
                  0 no cellular failure
                  0 no time failures
                  0 forced defunct socket
                  0 resumed socket
                  0 timeout expired failure
                  0 timer rescheduled
                  0 no delegated failure
            net_api:
                  2 interface filters currently attached
                  2 interface filters attached since boot
                  2 interface filters attached since boot by OS
                  0 IP filter currently attached
                  0 IP filter attached since boot
                  0 IP filter attached since boot by OS
                  4 socket filters currently attached
                  4 socket filters attached since boot
                  4 socket filters attached since boot by OS
                  26928 sockets allocated since boot
                  1 socket allocated in-kernel since boot
                  1 socket allocated in-kernel by OS
                  2575 sockets with NECP client UUID since boot
                  10196 local domain sockets allocated since boot
                  87 route domain sockets allocated since boot
                  9650 inet domain sockets allocated since boot
                  2575 inet6 domain sockets allocated since boot
                  861 system domain sockets allocated since boot
                  0 multipath domain socket allocated since boot
                  0 key domain socket allocated since boot
                  0 ndrv domain socket allocated since boot
                  0 other domains socket allocated since boot
                  4258 IPv4 stream sockets created since boot
                  5392 IPv4 datagram sockets created since boot
                  43 IPv4 datagram sockets connected
                  1656 IPv4 DNS sockets
                  3633 IPv4 datagram sockets without data
                  503 IPv6 stream sockets created since boot
                  2072 IPv6 datagram sockets created since boot
                  32 IPv6 datagram sockets connected
                  0 IPv6 DNS socket
                  2061 IPv6 datagram sockets without data
                  13 socket multicast joins since boot
                  13 socket multicast joins since boot by OS
                  0 IPv4 stream nexus flow added since boot
                  0 IPv4 datagram nexus flow added since boot
                  0 IPv6 stream nexus flow added since boot
                  0 IPv6 datagram nexus flow added since boot
                  12 interfaces currently allocated
                  38 interfaces allocated since boot
                  12 interfaces currently allocated by OS
                  38 extended interfaces allocated since boot by OS
                  2 PF addrule operations since boot
                  0 PF addrule operation since boot by OS
                  0 vmnet start since boot
