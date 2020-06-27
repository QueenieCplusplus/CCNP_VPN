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
 
        router#conf t
        
        router#hostname r2
        //輸入網路設備名稱
 
 (2) 在路由器上設定動態路由 EIGRP
 
    Host A        ----------      Router A    ---- WAN -----      Router B   GW 172.0.0.0    
    
                                                                     GW 192.168.0.0
 
        router#ip subnet-zero
        
        router#router eigrp 100
        
        router#network 172.0.0.0
        
        router#network 192.168.0.0
        
        router#no auto-summary
        
        ctrl + z
        
 
 (3)
 
 (4)
 
 (5)
 
 (6)
 
 (7)
 
 (8)
 
 (9)
 
 (10)
 
 (11)
 
 (12)
 
 (13)
 
 (14)



