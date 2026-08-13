# 🌐 Simulação de Rede Corporativa Multi-Filiais (SP e RJ)

**Autor:** Ralph Costa da Silva

## 📋 Sobre o Projeto
Este laboratório prático simula a infraestrutura de rede de uma corporação com matriz em São Paulo e uma filial no Rio de Janeiro. O objetivo principal foi aplicar conceitos de roteamento, segmentação de tráfego corporativo e políticas de segurança na camada de rede.

## 🛠️ Tecnologias e Protocolos Utilizados
* **Simulador:** Cisco Packet Tracer
* **Equipamentos:** Roteadores e Switches Cisco (IOS)
* **Comunicação:** Roteamento Estático entre localidades
* **Segmentação:** Criação e configuração de 8 VLANs distintas para o isolamento de departamentos
* **Segurança:** Implementação de Access Control Lists (ACLs) para restrição e filtro de tráfego interno

## 🏗️ Topologia da Rede
*(Observação: Substituir esta linha por um print nítido da topologia no Packet Tracer)*

## ⚙️ Destaques da Configuração (CLI)
Neste projeto, desenvolvi na prática a configuração dos equipamentos via linha de comando (CLI), resolvendo os seguintes desafios:
1. **Configuração de VLANs:** Separação lógica de 8 setores para reduzir domínios de broadcast, organizar o endereçamento IP e aumentar a segurança departamental.
2. **Roteamento de Filiais:** Estabelecimento e validação da comunicação de dados fim a fim entre as unidades de São Paulo e Rio de Janeiro.
3. **Filtros de Tráfego:** Criação de regras de ACL para permitir ou bloquear a comunicação de pacotes específicos entre as VLANs.

## 🚀 Como testar este laboratório
Os arquivos de configuração e o arquivo `.pkt` deste laboratório estão disponíveis neste repositório.
