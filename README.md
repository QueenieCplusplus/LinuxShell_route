# LinuxShell_route


* 查詢路由設定

usage

      route [args] cmd [[modifiers] args]
      
 * args
 
    （略）
 

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
          +---------------+-----------------------------+

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
      
      192.168.100.1      0:9:f:b9:4c:55     UHLWIir        en0   1177
      
      192.168.100.3      f0:99:b6:31:7:d3   UHLWI          en0     83
      192.168.100.13     1c:91:48:9d:49:c9  UHLWIi         en0   1012      
      192.168.100.24/32  link#4             UCS            en0      !
      
      192.168.100.255    ff:ff:ff:ff:ff:ff  UHLWbI         en0      !
      
      224.0.0/4          link#4             UmCS           en0      !
      224.0.0.251        1:0:5e:0:0:fd      UHmLWI         en0       
      
      255.255.255.255/32 link#4             UCS            en0      !
