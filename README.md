# 🌐 Infraestrutura de Rede Corporativa: Matriz (SP) e Filial (RJ)

**Autor:** Ralph Costa da Silva

## 📋 Sobre o Projeto
Este laboratório simula a infraestrutura de rede de uma corporação com matriz em São Paulo e filial no Rio de Janeiro. O objetivo é estabelecer a conectividade segura, escalável e de alta disponibilidade entre duas localidades, aplicando conceitos avançados de roteamento dinâmico, segmentação e telefonia IP.

## 🛠️ Tecnologias e Protocolos Utilizados
* **Simulador:** Cisco Packet Tracer
* **Equipamentos:** Roteadores (Cisco 2811) e Switches Cisco (IOS)
* **Roteamento Dinâmico:** OSPF (redes internas) e BGP (comunicação entre filiais)
* **Segmentação e Endereçamento:** Múltiplas VLANs, DHCP (IPv4) e SLAAC/DHCPv6 (IPv6)
* **Segurança Perimetral:** NAT, ACLs (Access Control Lists) estendidas para filtro de tráfego e acesso remoto seguro (SSH)
* **Serviços:** Telefonia IP (Cisco CallManager Express - VoIP)

## 🗺️ Topologia da Rede (Visão Global)
![Visão Global da Rede](Topologia%20Global.png)

## 🏢 Visão Detalhada: Matriz São Paulo (SP)
A infraestrutura da matriz concentra os servidores críticos (DNS, Produção) e o maior volume de VLANs departamentais, além do roteador principal responsável pelo NAT e regras de firewall perimetral.
![Topologia Matriz SP](Topologia%20SP.png)

## 🏖️ Visão Detalhada: Filial Rio de Janeiro (RJ)
A filial opera com estrutura espelhada de segmentação, destacando-se a integração de redes sem fio (Access Points) isoladas para visitantes e tráfego corporativo.
![Topologia Filial RJ](Topologia%20RJ.png)

## 🔗 O Coração da Rede: Link WAN e ISP
Comunicação estabelecida entre os roteadores Cisco 2811 através de roteamento dinâmico, garantindo a troca de rotas e a comunicação da Telefonia IP (VoIP) entre os estados.
![Topologia ISP](Topologia%20isp.png)

## 🚀 Destaques da Configuração (CLI)
Os arquivos `.txt` neste repositório contêm as configurações integrais (*show running-config*) dos roteadores principais. O foco da implementação foi garantir o *hardening* dos equipamentos, a comunicação inter-VLANs e o bloqueio estrito de redes sensíveis através de firewalls baseados em ACLs.

## 💻 Configurações dos Equipamentos (CLI)

<details>
<summary>🖱️ <b>Clique aqui para ver a configuração do Roteador Principal SP (show running-config)</b></summary>

```text
Roteador-Principal-SP#show running-config
Building configuration...

Current configuration : 15037 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Roteador-Principal-SP
!
!
!
enable secret 5 $1$mERr$4dpRATIgxQacPVK0CfNV4/
!
!
ip dhcp excluded-address 192.164.0.1
ip dhcp excluded-address 192.164.0.9
ip dhcp excluded-address 192.164.0.17
ip dhcp excluded-address 192.164.0.25
ip dhcp excluded-address 192.164.0.33
ip dhcp excluded-address 192.164.0.41
ip dhcp excluded-address 192.164.0.49
ip dhcp excluded-address 192.164.0.65
ip dhcp excluded-address 192.164.0.81
ip dhcp excluded-address 192.164.0.36
ip dhcp excluded-address 192.164.0.44
ip dhcp excluded-address 192.164.0.19
ip dhcp excluded-address 192.164.0.18
!
ip dhcp pool vlan10
 network 192.164.0.0 255.255.255.248
 default-router 192.164.0.1
 dns-server 192.164.0.69
ip dhcp pool vlan20
 network 192.164.0.8 255.255.255.248
 default-router 192.164.0.9
 dns-server 192.164.0.69
ip dhcp pool vlan30
 network 192.164.0.16 255.255.255.248
 default-router 192.164.0.17
 dns-server 192.164.0.69
ip dhcp pool vlan40
 network 192.164.0.24 255.255.255.248
 default-router 192.164.0.25
 dns-server 192.164.0.69
ip dhcp pool vlan50
 network 192.164.0.32 255.255.255.248
 default-router 192.164.0.33
 dns-server 192.164.0.69
ip dhcp pool vlan60
 network 192.164.0.40 255.255.255.248
 default-router 192.164.0.41
 dns-server 192.164.0.69
ip dhcp pool vlan70
 network 192.164.0.48 255.255.255.240
 default-router 192.164.0.49
 dns-server 192.164.0.69
ip dhcp pool vlan80
 network 192.164.0.64 255.255.255.248
 default-router 192.164.0.65
ip dhcp pool vlan90
 network 192.164.0.80 255.255.255.240
 default-router 192.164.0.81
 option 150 ip 192.164.0.81
ip dhcp pool vlan100
 network 192.164.0.96 255.255.255.248
 default-router 192.164.0.97
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
ipv6 dhcp pool vlan10p
 address prefix 2026:ac64:509e:1::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan20p
 address prefix 2026:ac64:509e:2::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan30p
 address prefix 2026:ac64:509e:3::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan40p
 address prefix 2026:ac64:509e:4::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan50p
 address prefix 2026:ac64:509e:5::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan60p
 address prefix 2026:ac64:509e:6::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan70p
 address prefix 2026:AC64:509E:7::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
!
!
username admin privilege 15 secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
license udi pid CISCO2811/K9 sn FTX1017G3EA-
!
!
!
!
!
!
!
!
!
!
!
ip ssh version 2
ip domain-name empresa.com
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/0
 no ip address
 duplex auto
 speed auto
!
interface FastEthernet0/0.1
 encapsulation dot1Q 10
 ip address 192.164.0.1 255.255.255.248
 ip nat inside
 ip access-group vlan10 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:AC64:509E:1::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan10p
!
interface FastEthernet0/0.2
 encapsulation dot1Q 20
 ip address 192.164.0.9 255.255.255.248
 ip nat inside
 ip access-group vlan20 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:AC64:509E:2::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan20p
!
interface FastEthernet0/0.3
 encapsulation dot1Q 30
 ip address 192.164.0.17 255.255.255.248
 ip nat inside
 ip access-group vlan30 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:AC64:509E:3::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan30p
!
interface FastEthernet0/0.4
 encapsulation dot1Q 40
 ip address 192.164.0.25 255.255.255.248
 ip nat inside
 ip access-group vlan40 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:AC64:509E:4::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan40p
!
interface FastEthernet0/0.5
 encapsulation dot1Q 50
 ip address 192.164.0.33 255.255.255.248
 ip nat inside
 ip access-group vlan50 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:AC64:509E:5::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan50p
!
interface FastEthernet0/0.6
 encapsulation dot1Q 60
 ip address 192.164.0.41 255.255.255.248
 ip nat inside
 ip access-group vlan60 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:AC64:509E:6::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan60p
!
interface FastEthernet0/0.7
 encapsulation dot1Q 70
 ip address 192.164.0.49 255.255.255.240
 ip nat inside
 ip access-group vlan70 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:AC64:509E:7::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan70p
!
interface FastEthernet0/0.8
 encapsulation dot1Q 80
 ip address 192.164.0.65 255.255.255.248
 ip nat inside
 ipv6 address 2026:AC64:509E:8::1/64
!
interface FastEthernet0/0.9
 encapsulation dot1Q 90
 ip address 192.164.0.81 255.255.255.240
!
interface FastEthernet0/0.10
 encapsulation dot1Q 100
 ip address 192.164.0.97 255.255.255.248
 ip nat inside
!
interface FastEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 ip address 200.2.0.1 255.255.255.252
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/3/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/3/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 log-adjacency-changes
 redistribute bgp 2002 subnets 
 network 200.2.0.0 0.0.0.255 area 0
 network 192.164.0.0 0.0.0.255 area 0
!
router bgp 2002
 bgp log-neighbor-changes
 no synchronization
 neighbor 200.2.0.2 remote-as 2000
 redistribute ospf 1 
!
ip nat inside source list nat interface Serial0/1/0 overload
ip nat inside source list nat1 interface Serial0/1/0 overload
ip nat inside source list nat1.0 interface Serial0/1/0 overload
ip classless
ip route 200.0.0.0 255.255.255.252 Serial0/1/0 
!
ip flow-export version 9
!
!
ip access-list extended nat1.0
 deny ip 192.164.0.80 0.0.0.15 any
 deny ip 192.164.0.80 0.0.0.15 192.168.0.48 0.0.0.15
 deny ip 192.164.0.0 0.0.0.7 192.168.0.0 0.0.0.255
 deny ip 192.164.0.0 0.0.0.15 192.168.0.0 0.0.0.255
 permit ip 192.164.0.0 0.0.0.255 any
ip access-list extended vlan70
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.164.0.48 0.0.0.15 192.164.0.96 0.0.0.7 established
 permit icmp 192.164.0.48 0.0.0.15 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.164.0.48 0.0.0.15 host 192.164.0.67 eq www
 permit icmp 192.164.0.48 0.0.0.15 host 192.164.0.67
 permit tcp 192.164.0.48 0.0.0.15 host 192.164.0.3 eq smtp
 permit ip 192.164.0.48 0.0.0.7 host 192.164.0.69
 permit tcp 192.164.0.48 0.0.0.15 host 192.164.0.3 eq 445
 permit icmp 192.164.0.48 0.0.0.15 host 192.164.0.3
 permit tcp 192.164.0.48 0.0.0.15 host 192.164.0.2 eq smtp
 permit tcp 192.164.0.48 0.0.0.15 host 192.164.0.2 eq 445
 permit icmp 192.164.0.48 0.0.0.15 host 192.164.0.2
 deny ip 192.164.0.48 0.0.0.15 192.164.0.96 0.0.0.7
 deny ip 192.164.0.48 0.0.0.15 192.164.0.0 0.0.0.7
 deny ip 192.164.0.48 0.0.0.15 192.168.0.0 0.0.0.255
 permit ip 192.164.0.48 0.0.0.15 any
ip access-list extended vlan30
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit icmp 192.164.0.16 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.164.0.16 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit tcp 192.164.0.16 0.0.0.7 host 192.164.0.68 eq www
 permit ip 192.164.0.16 0.0.0.7 host 192.164.0.69
 permit tcp 192.164.0.16 0.0.0.7 192.164.0.24 0.0.0.7 eq smtp
 permit tcp 192.164.0.16 0.0.0.7 host 192.164.0.36 eq smtp
 permit tcp 192.164.0.16 0.0.0.7 host 192.164.0.44 eq smtp
 permit tcp 192.164.0.16 0.0.0.7 host 192.164.0.2 eq smtp
 permit tcp 192.164.0.16 0.0.0.7 host 192.164.0.3 eq smtp
 permit icmp 192.164.0.16 0.0.0.7 host 192.164.0.68
 permit icmp 192.164.0.16 0.0.0.7 192.164.0.24 0.0.0.7
 permit icmp 192.164.0.16 0.0.0.7 host 192.164.0.36
 permit icmp 192.164.0.16 0.0.0.7 host 192.164.0.44
 permit icmp 192.164.0.16 0.0.0.7 host 192.164.0.2
 permit icmp 192.164.0.16 0.0.0.7 host 192.164.0.3
 permit ip 192.164.0.16 0.0.0.7 192.168.0.16 0.0.0.7
 deny ip 192.164.0.16 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.164.0.16 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.164.0.16 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.164.0.16 0.0.0.7 any
ip access-list extended vlan40
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.164.0.24 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.164.0.24 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.164.0.24 0.0.0.7 192.164.0.16 0.0.0.7 eq smtp
 permit ip 192.164.0.24 0.0.0.7 host 192.164.0.69
 permit tcp 192.164.0.24 0.0.0.7 host 192.164.0.68 eq www
 permit tcp 192.164.0.24 0.0.0.7 host 192.164.0.36 eq smtp
 permit tcp 192.164.0.24 0.0.0.7 host 192.164.0.44 eq smtp
 permit tcp 192.164.0.24 0.0.0.7 host 192.164.0.2 eq smtp
 permit tcp 192.164.0.24 0.0.0.7 host 192.164.0.3 eq smtp
 permit tcp 192.164.0.24 0.0.0.7 host 192.168.0.26 eq smtp
 permit icmp 192.164.0.24 0.0.0.7 host 192.164.0.68
 permit icmp 192.164.0.24 0.0.0.7 192.164.0.16 0.0.0.7
 permit icmp 192.164.0.24 0.0.0.7 host 192.164.0.36
 permit icmp 192.164.0.24 0.0.0.7 host 192.164.0.44
 permit icmp 192.164.0.24 0.0.0.7 host 192.164.0.2
 permit icmp 192.164.0.24 0.0.0.7 host 192.164.0.3
 permit icmp 192.164.0.24 0.0.0.7 host 192.168.0.26
 deny ip 192.164.0.24 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.164.0.24 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.164.0.24 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.164.0.24 0.0.0.7 any
ip access-list extended vlan50
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.164.0.32 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.164.0.32 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.164.0.32 0.0.0.7 host 192.164.0.66 eq www
 permit ip 192.164.0.32 0.0.0.7 host 192.164.0.69
 permit tcp host 192.164.0.36 192.164.0.16 0.0.0.7 eq smtp
 permit tcp 192.164.0.32 0.0.0.7 192.164.0.40 0.0.0.7 eq smtp
 permit tcp 192.164.0.32 0.0.0.7 192.164.0.40 0.0.0.7 eq 445
 permit tcp 192.164.0.32 0.0.0.7 192.168.0.0 0.0.0.15 eq smtp
 permit tcp 192.164.0.32 0.0.0.7 192.168.0.0 0.0.0.15 eq 445
 permit icmp 192.164.0.32 0.0.0.7 host 192.164.0.66
 permit icmp 192.164.0.32 0.0.0.7 192.164.0.40 0.0.0.7
 permit icmp host 192.164.0.36 192.164.0.16 0.0.0.7
 permit icmp 192.164.0.32 0.0.0.7 192.168.0.0 0.0.0.15
 deny ip 192.164.0.32 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.164.0.32 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.164.0.32 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.164.0.32 0.0.0.7 any
ip access-list extended vlan60
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.164.0.40 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.164.0.40 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.164.0.40 0.0.0.7 host 192.164.0.66 eq www
 permit ip 192.164.0.40 0.0.0.7 host 192.164.0.69
 permit tcp host 192.164.0.44 192.164.0.16 0.0.0.7 eq smtp
 permit tcp 192.164.0.40 0.0.0.7 192.164.0.32 0.0.0.7 eq smtp
 permit tcp 192.164.0.40 0.0.0.7 192.164.0.32 0.0.0.7 eq 445
 permit tcp 192.164.0.40 0.0.0.7 192.168.0.0 0.0.0.15 eq smtp
 permit tcp 192.164.0.40 0.0.0.7 192.168.0.0 0.0.0.15 eq 445
 permit icmp 192.164.0.40 0.0.0.7 host 192.164.0.66
 permit icmp 192.164.0.40 0.0.0.7 192.164.0.32 0.0.0.7
 permit icmp host 192.164.0.44 192.164.0.16 0.0.0.7
 permit icmp 192.164.0.40 0.0.0.7 192.168.0.0 0.0.0.15
 deny ip 192.164.0.40 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.164.0.40 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.164.0.40 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.164.0.40 0.0.0.7 any
ip access-list extended vlan10
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.164.0.0 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.164.0.0 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.164.0.0 0.0.0.7 host 192.164.0.67 eq www
 permit ip 192.164.0.0 0.0.0.7 host 192.164.0.69
 permit tcp 192.164.0.0 0.0.0.7 192.164.0.16 0.0.0.7 eq smtp
 permit tcp 192.164.0.0 0.0.0.7 192.164.0.24 0.0.0.7 eq smtp
 permit tcp 192.164.0.0 0.0.0.7 192.164.0.48 0.0.0.7 eq smtp
 permit tcp 192.164.0.0 0.0.0.7 192.164.0.48 0.0.0.7 eq 445
 permit tcp 192.164.0.0 0.0.0.7 192.164.0.8 0.0.0.7 eq smtp
 permit tcp 192.164.0.0 0.0.0.7 192.164.0.8 0.0.0.7 eq 445
 permit tcp 192.164.0.0 0.0.0.7 192.168.0.32 0.0.0.7 eq smtp
 permit icmp 192.164.0.0 0.0.0.7 host 192.164.0.67
 permit icmp 192.164.0.0 0.0.0.7 192.164.0.16 0.0.0.7
 permit icmp 192.164.0.0 0.0.0.7 192.164.0.24 0.0.0.7
 permit icmp 192.164.0.0 0.0.0.7 192.164.0.48 0.0.0.7
 permit icmp 192.164.0.0 0.0.0.7 192.164.0.8 0.0.0.7
 permit icmp 192.164.0.0 0.0.0.7 192.168.0.32 0.0.0.7
 deny ip 192.164.0.0 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.164.0.0 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.164.0.0 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.164.0.0 0.0.0.7 any
ip access-list extended vlan20
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.164.0.8 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.164.0.8 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.164.0.8 0.0.0.7 192.164.0.0 0.0.0.7 eq smtp
 permit ip 192.164.0.8 0.0.0.7 host 192.164.0.69
 permit tcp 192.164.0.8 0.0.0.7 192.164.0.0 0.0.0.7 eq 445
 permit tcp 192.164.0.8 0.0.0.7 192.168.0.32 0.0.0.7 eq smtp
 permit icmp 192.164.0.8 0.0.0.7 192.164.0.0 0.0.0.7
 permit icmp 192.164.0.8 0.0.0.7 192.168.0.32 0.0.0.7
 deny ip 192.164.0.8 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.164.0.8 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.164.0.8 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.164.0.8 0.0.0.7 any
ip access-list standard vlan100
 permit host 192.164.0.98
 deny any
!
!
!
!
!
dial-peer voice 10 voip
 destination-pattern 200[1-4]
 session target ipv4:192.168.0.49
!
telephony-service
 max-ephones 10
 max-dn 10
 ip source-address 192.164.0.81 port 2000
 auto assign 1 to 10
!
ephone-dn 1
 number 1001
!
ephone-dn 2
 number 1002
!
ephone-dn 3
 number 1003
!
ephone-dn 4
 number 1004
!
ephone 1
 device-security-mode none
 mac-address 0004.9AC6.8CCA
 type 7960
 button 1:1
!
ephone 2
 device-security-mode none
 mac-address 0002.179B.B865
 type 7960
 button 1:2
!
ephone 3
 device-security-mode none
 mac-address 00D0.FF8C.212E
 type 7960
 button 1:3
!
line con 0
!
line aux 0
!
line vty 0 4
 access-class vlan100 in
 login local
 transport input ssh
line vty 5 15
 access-class vlan100 in
 login local
 transport input ssh
!
!
!
end


<details>
<summary>🖱️ <b>Clique aqui para ver a configuração do Roteador Principal RJ (show running-config)</b></summary>

```text
Roteador-Principal-RJ#show running-config
Building configuration...

Current configuration : 9916 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Roteador-Principal-RJ
!
!
!
enable secret 5 $1$mERr$4dpRATIgxQacPVK0CfNV4/
!
!
ip dhcp excluded-address 192.168.0.1
ip dhcp excluded-address 192.168.0.17
ip dhcp excluded-address 192.168.0.25
ip dhcp excluded-address 192.168.0.33
ip dhcp excluded-address 192.168.0.41
ip dhcp excluded-address 192.168.0.49
ip dhcp excluded-address 192.168.0.4
ip dhcp excluded-address 192.168.0.2
!
ip dhcp pool vlan10
 network 192.168.0.0 255.255.255.240
 default-router 192.168.0.1
 dns-server 192.164.0.69
ip dhcp pool vlan20
 network 192.168.0.16 255.255.255.248
 default-router 192.168.0.17
 dns-server 192.164.0.69
ip dhcp pool vlan30
 network 192.168.0.24 255.255.255.248
 default-router 192.168.0.25
 dns-server 192.164.0.69
ip dhcp pool vlan40
 network 192.168.0.32 255.255.255.248
 default-router 192.168.0.33
 dns-server 192.164.0.69
ip dhcp pool vlan50
 network 192.168.0.40 255.255.255.248
 default-router 192.168.0.41
ip dhcp pool vlan60
 network 192.168.0.48 255.255.255.240
 default-router 192.168.0.49
 option 150 ip 192.168.0.49
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
ipv6 dhcp pool vlan10p
 address prefix 2026:BC64:509E:1::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan20p
 address prefix 2026:BC64:509E:2::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan30p
 address prefix 2026:BC64:509E:3::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan40p
 address prefix 2026:BC64:509E:4::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
ipv6 dhcp pool vlan50p
 address prefix 2026:BC64:509E:5::/64 lifetime 172800 86400
 dns-server 2026:AC64:509E:8::2
!
!
!
username admin privilege 15 secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
license udi pid CISCO2811/K9 sn FTX1017H02B-
!
!
!
!
!
!
!
!
!
!
!
ip ssh version 2
ip domain-name empresarj.com
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/0
 no ip address
 duplex auto
 speed auto
!
interface FastEthernet0/0.1
 encapsulation dot1Q 10
 ip address 192.168.0.1 255.255.255.240
 ip nat inside
 ip access-group vlan10 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:BC64:509E:1::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan10p
!
interface FastEthernet0/0.2
 encapsulation dot1Q 20
 ip address 192.168.0.17 255.255.255.248
 ip nat inside
 ip access-group vlan20 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:BC64:509E:2::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan20p
!
interface FastEthernet0/0.3
 encapsulation dot1Q 30
 ip address 192.168.0.25 255.255.255.248
 ip nat inside
 ip access-group vlan30 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:BC64:509E:3::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan30p
!
interface FastEthernet0/0.4
 encapsulation dot1Q 40
 ip address 192.168.0.33 255.255.255.248
 ip nat inside
 ip access-group vlan40 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:BC64:509E:4::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan40p
!
interface FastEthernet0/0.5
 encapsulation dot1Q 50
 ip address 192.168.0.41 255.255.255.248
 ip nat inside
 ip access-group vlan50 in
 ipv6 address FE80::1 link-local
 ipv6 address 2026:BC64:509E:5::1/64
 ipv6 nd managed-config-flag
 ipv6 dhcp server vlan50p
!
interface FastEthernet0/0.6
 encapsulation dot1Q 60
 ip address 192.168.0.49 255.255.255.240
!
interface FastEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 ip address 200.1.0.1 255.255.255.252
 ip nat outside
 clock rate 2000000
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 log-adjacency-changes
 redistribute bgp 2001 subnets 
 network 200.1.0.0 0.0.0.255 area 0
 network 192.168.0.0 0.0.0.255 area 0
!
router bgp 2001
 bgp log-neighbor-changes
 no synchronization
 neighbor 200.1.0.2 remote-as 2000
 redistribute ospf 1 
!
ip nat inside source list nat interface Serial0/1/0 overload
ip nat inside source list nat1 interface Serial0/1/0 overload
ip nat inside source list nat1.0 interface Serial0/1/0 overload
ip classless
ip route 200.0.0.0 255.255.255.252 Serial0/1/0 
!
ip flow-export version 9
!
!
ip access-list extended nat1.0
 deny ip 192.168.0.48 0.0.0.15 any
 deny ip 192.168.0.48 0.0.0.15 192.164.0.80 0.0.0.15
 deny ip 192.164.0.0 0.0.0.7 192.168.0.0 0.0.0.255
 deny ip 192.164.0.0 0.0.0.15 192.168.0.0 0.0.0.255
 permit ip 192.164.0.0 0.0.0.255 any
ip access-list extended vlan10
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.168.0.0 0.0.0.15 192.164.0.96 0.0.0.7 established
 permit icmp 192.168.0.0 0.0.0.15 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.168.0.0 0.0.0.15 host 192.164.0.66 eq www
 permit ip 192.168.0.0 0.0.0.15 host 192.164.0.69
 permit tcp host 192.168.0.4 192.168.0.16 0.0.0.7 eq smtp
 permit tcp host 192.168.0.2 192.168.0.16 0.0.0.7 eq smtp
 permit tcp 192.168.0.0 0.0.0.15 192.164.0.40 0.0.0.7 eq smtp
 permit tcp 192.168.0.0 0.0.0.15 192.164.0.40 0.0.0.7 eq 445
 permit tcp 192.168.0.0 0.0.0.15 192.164.0.32 0.0.0.7 eq smtp
 permit tcp 192.168.0.0 0.0.0.15 192.164.0.32 0.0.0.7 eq 445
 permit icmp 192.168.0.0 0.0.0.15 host 192.164.0.66
 permit icmp host 192.168.0.4 192.168.0.16 0.0.0.7
 permit icmp host 192.168.0.2 192.168.0.16 0.0.0.7
 permit icmp 192.168.0.0 0.0.0.15 192.164.0.40 0.0.0.7
 permit icmp 192.168.0.0 0.0.0.15 192.164.0.32 0.0.0.7
 deny ip 192.168.0.0 0.0.0.15 192.164.0.96 0.0.0.7
 deny ip 192.168.0.0 0.0.0.15 192.164.0.0 0.0.0.255
 deny ip 192.168.0.0 0.0.0.15 192.168.0.0 0.0.0.255
 permit ip 192.168.0.0 0.0.0.15 any
ip access-list extended vlan20
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.168.0.16 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.168.0.16 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.168.0.16 0.0.0.7 host 192.164.0.68 eq www
 permit ip 192.168.0.16 0.0.0.7 host 192.164.0.69
 permit tcp 192.168.0.16 0.0.0.7 host 192.168.0.4 eq smtp
 permit tcp 192.168.0.16 0.0.0.7 host 192.168.0.2 eq smtp
 permit ip 192.168.0.16 0.0.0.7 192.164.0.16 0.0.0.7
 permit icmp 192.168.0.16 0.0.0.7 host 192.164.0.68
 permit icmp 192.168.0.16 0.0.0.7 host 192.168.0.4
 permit icmp 192.168.0.16 0.0.0.7 host 192.168.0.2
 permit icmp 192.168.0.16 0.0.0.7 192.164.0.16 0.0.0.7
 deny ip 192.168.0.16 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.168.0.16 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.168.0.16 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.168.0.16 0.0.0.7 any
ip access-list extended vlan30
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.164.0.69 eq domain
 permit tcp 192.168.0.24 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.168.0.24 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.168.0.24 0.0.0.7 host 192.164.0.68 eq www
 permit ip 192.168.0.24 0.0.0.7 host 192.164.0.69
 permit tcp 192.168.0.24 0.0.0.7 host 192.168.0.16 eq smtp
 permit tcp 192.168.0.24 0.0.0.7 host 192.168.0.4 eq smtp
 permit tcp 192.168.0.24 0.0.0.7 host 192.168.0.2 eq smtp
 permit tcp 192.168.0.24 0.0.0.7 host 192.168.0.36 eq smtp
 permit tcp 192.168.0.24 0.0.0.7 192.164.0.24 0.0.0.7 eq smtp
 permit icmp 192.168.0.24 0.0.0.7 host 192.164.0.68
 permit icmp 192.168.0.24 0.0.0.7 host 192.168.0.16
 permit icmp 192.168.0.24 0.0.0.7 host 192.168.0.4
 permit icmp 192.168.0.24 0.0.0.7 host 192.168.0.2
 permit icmp 192.168.0.24 0.0.0.7 host 192.168.0.36
 permit icmp 192.168.0.24 0.0.0.7 192.164.0.24 0.0.0.7
 deny ip 192.168.0.24 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.168.0.24 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.168.0.24 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.168.0.24 0.0.0.7 any
ip access-list extended vlan40
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit tcp host 192.168.0.36 192.168.0.16 0.0.0.7 eq smtp
 permit tcp 192.168.0.32 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.168.0.32 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 permit tcp 192.168.0.32 0.0.0.7 192.164.0.8 0.0.0.7 eq smtp
 permit tcp 192.168.0.32 0.0.0.7 192.164.0.0 0.0.0.7 eq smtp
 permit icmp host 192.168.0.36 192.168.0.16 0.0.0.7
 permit icmp 192.168.0.32 0.0.0.7 192.164.0.8 0.0.0.7
 permit icmp 192.168.0.32 0.0.0.7 192.164.0.0 0.0.0.7
 deny ip 192.168.0.32 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.168.0.32 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.168.0.32 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.168.0.32 0.0.0.7 any
ip access-list extended vlan50
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit tcp 192.168.0.40 0.0.0.7 192.164.0.96 0.0.0.7 established
 permit icmp 192.168.0.40 0.0.0.7 192.164.0.96 0.0.0.7 echo-reply
 deny ip 192.168.0.40 0.0.0.7 192.164.0.96 0.0.0.7
 deny ip 192.168.0.40 0.0.0.7 192.164.0.0 0.0.0.255
 deny ip 192.168.0.40 0.0.0.7 192.168.0.0 0.0.0.255
 permit ip 192.168.0.40 0.0.0.7 any
ip access-list standard vlan100
 permit host 192.164.0.98
 deny any
!
!
!
!
!
dial-peer voice 11 voip
 destination-pattern 200[1-4]
 session target ipv4:192.164.0.81
!
dial-peer voice 20 voip
 destination-pattern 100[1-4]
 session target ipv4:192.164.0.81
!
telephony-service
 max-ephones 10
 max-dn 10
 ip source-address 192.168.0.49 port 2000
 auto assign 1 to 10
!
ephone-dn 1
 number 2001
!
ephone-dn 2
 number 2002
!
ephone-dn 3
 number 2003
!
ephone-dn 4
 number 2004
!
ephone 1
 device-security-mode none
 mac-address 0060.5C0C.4AB2
 type 7960
 button 1:1
!
ephone 2
 device-security-mode none
 mac-address 00E0.F914.B6CA
 type 7960
 button 1:2
!
line con 0
!
line aux 0
!
line vty 0 4
 access-class vlan100 in
 login local
 transport input ssh
line vty 5 15
 access-class vlan100 in
 login local
 transport input ssh
!
!
!
end
