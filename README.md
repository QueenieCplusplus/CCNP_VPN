# CCNP VPN
虛擬私有網路

# 核心技術

* Tunneling, 通道技術

* Ciphor, 加解密技術

* Key Mgmt, 金鑰管理

* Auth, 認證技術

# 實際操作

 
 
    Host A        ----------      Router A    ---- WAN -----      Router B     ---------    Host B
     
     
 
 (1) 在電腦 B 上用 console line 連接路由器 B ，開啟 terminal，進入 Priviledge 模式
 
        routerB#conf t
        
        routerB(config)#hostname r2
        //注意游標的變化
        //輸入網路設備名稱
 
 (2) 在路由器上設定動態路由 EIGRP
 
    Host A        ----------      Router A    ---- WAN -----      Router B   GW 172.0.0.0    
    
                                                                     GW 192.168.0.0
 
        routerB(config)#ip subnet-zero
        
        routerB(config)#router eigrp 100
        
        routerB(config-router)#network 172.0.0.0
        // 注意游標的變化
        
        routerB(config-router)#network 192.168.0.0
        
        routerB(config-router)#no auto-summary
        
        ctrl + z
        
        router#
        
 
 (3) 設定路由器的 IP 位址
 
                                                                    
                                                                   192.168.0.2
                                                                      |
                                                                   int s0
     Host A        ----------      Router A    ---- WAN -----      Router B - GW 172.0.0.0    
    

       routerB#conf t
       
       routerB(config)# int s0
       
       routerB(config-if)#ip addr 192.168.0.2 255.255.255.0
       
       routerB(config-if)#no shutdown
       
       routerB(config-if)#clock rate 64000
       
       ctrl + Z
                                                                                                                         
 
 (4) 測試連線 Router B ------ Router A
     在 Router B 上使用 ping 至 Router A 的 IP 位址。
 
 
                                                                    192.168.0.2
                                                                      |
                                 192.168.0.1                        int s0
     Host A        ----------      Router A    ---- WAN -----      Router B - GW 172.0.0.0   
     
     
        routerB#ping 192.168.0.1
     
 
 (5) 設定通道，其編號為 O
 
 
                                                                     192.168.0.2
                                                                      |
                                 192.168.0.1                        int s0
     Host A        ----------      Router A    ---- WAN -----      Router B - GW 172.0.0.0   
     
                                     to0 --------------------------- to0
                                    192.168.1.1                      192.168.1.2
 
 
        routerB#conf t
        routerB(config)#int tunnel 0
        
        routerB(config-if)#tunnel source 192.168.0.2
        
        routerB(config-if)#tunnel destination 192.168.0.1
        
        routerB(config-if)#ip address 192.168.1.2 255.255.255.0
        
        ctrl + Z
 
 
 (6) 測試通道連線是否順利
 
       routerB#ping 192.168.1.1
 
 (7) 觀察通道訊息
 
      routerB#sh int tunnel 0
      
      Tunnel0 is up, line protocol is up.
 
 (8) 檢視除錯功能是否開啟
 
      routerB#debug tunnel 
      
      Tunnel Interface dbugging is on.
 
 (9) 藉由 ping 通道預設的目標 IP 位址，觀察封包的加解封裝情況
 
 (10) 藉由 ping 對方路由器的 IP 位址，查看是否連通
 
 (11) 開啟檢驗總和 checksum 、通道鑰 key、順序的資料報
 
       routerB#conf t
       
       routerB(config)#int tunnel 0
       
       routerB(conf-if)#tunnel checksum
       
       routerB(conf-if)#tunnel key 31877
       
       routerB(conf-if)#tunnel sequence-datagrams
       
       ctrl + Z
  
 (12)
 
 (13)
 
 (14)



