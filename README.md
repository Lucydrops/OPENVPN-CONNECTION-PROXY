# OPENVPN-reverse-proxy
See a  lot of people ask how to set up a reverse proxy for the openvpn connection so i found out how to do it and thought why not share it here.

thanks to Brad for showing me how to do this.

___________________________________________________________________________________________________________________________________

allowing ip forwarding

first if all we need to allow IP forwarding 

```sysctl -w net.ipv4.ip_forward=1```
___________________________________________________________________________________________________________________________________

opening the port

```open up the port you want to connect to on both servers *preferably on the network level* in this case we will be using 1194```
___________________________________________________________________________________________________________________________________

routing

```iptables -t nat -I PREROUTING 1 -d 0.0.0.0/0 -p tcp --dport 1194 -j DNAT --to-dest regularip:port```

```iptables -t nat -I POSTROUTING 1 -d regularip -p tcp --dport 1194 -j SNAT --to-source proxyip```

```iptables -I FORWARD 1 -d regularip -p tcp --dport 1194 -j ACCEPT```


___________________________________________________________________________________________________________________________________

installing OPENVPN

```curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh```

```chmod +x openvpn-install.sh```

```./openvpn-install.sh```

paste these in to run the openvpn installer script made by angristan

once you go through the install make sure to use tcp if your following this guide directly and make sure to use the port that you opened up.


___________________________________________________________________________________________________________________________________


configuring the OPENVPN file


once you have downloaded the file open it up in notepad and change the part where it shows the ip and port 
and change it to the proxy ip

___________________________________________________________________________________________________________________________________


CONNECT!!

now all there is left to do is connect to the client and if all is working you should connect fine!


___________________________________________________________________________________________________________________________________








