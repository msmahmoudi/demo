
Implementation Plan:
1. Email IBM NETOPS and GNS@scotiabank.com  to notify the change
2. Save the existing running configuration on F5 load balancer and the backup on my laptop.
3. Logon the network devices and apply the change
4. Check and verify the configuration change and run best network level testing 
5. Email IBM NETOPS and GNS@scotiabank.com to check if there is any related alert after change
6. Save the new running configuration on devices and the backup on my laptop


Device list:





create ltm node  address  description 




create ltm pool  members add { } monitor TCP_10_10_31_31



create ltm virtual  destination  profiles add { tcp-lan-optimized } source-address-translation { type automap } pool 



modify ltm virtual-address  route-advertisement enabled icmp-echo selective


save sys config





	#create ltm node 192.168.43.217 address 192.168.43.217 description sbuld2wm080.bcp.bns	
    #create ltm pool logs.uat.digitalbanking.balabit-splunk.bns_6003 members add {172.25.158.204:6003  172.25.158.205:6003 } monitor TCP_10_10_31_31
	#create ltm virtual VS-logs.uat.digitalbanking.balabit-splunk.bns_6003 destination 192.168.94.113:6003 profiles add { tcp-lan-optimized } source-address-translation { type automap } pool logs.uat.digitalbanking.balabit-splunk.bns_6003
	#modify ltm virtual-address 192.168.94.113 route-advertisement enabled icmp-echo selective





create ltm profile client-ssl banking.blue.uat.cloud-f5-sol.bns 
{
      ca-file New-BNS-Chain.crt 
      peer-cert-mode require 
      cert banking.blue.uat.cloud-f5-sol.bns.crt 
      key banking.blue.uat.cloud-f5-sol.bns.key 
      chain BNS_Bundle.crt 
      ciphers DEFAULT:!TLSv1:!TLSv1_1:!DTLSv1:!DES-CBC3-SHA:!RC4:!ECDHE-RSA-DES-CBC3-SHA 
      defaults-from clientssl_strong_cipher
}



CSR Information:
Common Name: nft.cloud-f5-sol.bns
Subject Alternative Names: 
banking.blue.nft.cloud-f5-sol.bns, 
brokerage.blue.nft.cloud-f5-sol.bns, 
shared.blue.nft.cloud-f5-sol.bns, 
bondinventory.blue.nft.cloud-f5-sol.bns, 
wealth.blue.nft.cloud-f5-sol.bns, 
banking.orange.nft.cloud-f5-sol.bns, 
brokerage.orange.nft.cloud-f5-sol.bns, 
shared.orange.nft.cloud-f5-sol.bns, 
bondinventory.orange.nft.cloud-f5-sol.bns, 
wealth.orange.nft.cloud-f5-sol.bns, 
nft.cloud-f5-sol.bns



