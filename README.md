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

## 🗺️ Topologia da Rede
*(Substituiremos esta linha pela imagem da topologia no próximo passo)*

## 🚀 Destaques da Configuração (CLI)
Os arquivos `.txt` neste repositório contêm as configurações integrais (*show running-config*) dos roteadores principais. O foco da implementação foi garantir o *hardening* dos equipamentos, a comunicação inter-VLANs e o bloqueio estrito de redes sensíveis através de firewalls baseados em ACLs.
