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

    netstat -n

      ✗ netstat
      Active Internet connections
      Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)    
      tcp4       0      0  192.168.100.24.50346   tsa01s07-in-f10..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50345   tsa01s07-in-f10..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50344   nrt13s51-in-f14..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50343   tsa03s06-in-f10..https ESTABLISHED
      tcp4       0      0  192.168.100.24.50342   nrt13s51-in-f14..https ESTABLISHED
