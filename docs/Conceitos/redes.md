
# Redes de Computadores

## Introdução

Redes de computadores são sistemas interconectados que permitem a comunicação entre dispositivos computacionais, possibilitando o compartilhamento de recursos, dados e serviços. Essas redes formam a base da internet moderna e são fundamentais para a computação distribuída.

## Tipos de Redes

### Por Abrangência Geográfica

#### LAN (Local Area Network)
- **Definição**: Rede de área local que conecta dispositivos em uma área limitada
- **Alcance**: Geralmente dentro de um edifício ou campus
- **Características**: Alta velocidade, baixa latência, controle centralizado
- **Exemplos**: Rede doméstica, rede corporativa de um escritório

#### WAN (Wide Area Network)
- **Definição**: Rede de longa distância que conecta LANs em áreas geograficamente distantes
- **Alcance**: Cidades, países ou continentes
- **Características**: Velocidades variáveis, maior latência
- **Exemplos**: Internet, redes corporativas multinacionais

#### MAN (Metropolitan Area Network)
- **Definição**: Rede metropolitana que cobre uma cidade ou região metropolitana
- **Alcance**: Entre LAN e WAN em termos de cobertura
- **Características**: Conecta múltiplas LANs em uma área urbana

### Por Topologia

#### Topologia em Estrela
- **Estrutura**: Todos os dispositivos conectam-se a um hub ou switch central
- **Vantagens**: Fácil gerenciamento, falha isolada
- **Desvantagens**: Ponto único de falha (hub central)

#### Topologia em Anel
- **Estrutura**: Dispositivos conectados em formato circular
- **Vantagens**: Sem colisões, transmissão unidirecional
- **Desvantagens**: Falha em um nó afeta toda a rede

#### Topologia em Barramento
- **Estrutura**: Todos os dispositivos conectados a um cabo principal
- **Vantagens**: Simples e econômica
- **Desvantagens**: Colisões frequentes, difícil manutenção

#### Topologia Mesh
- **Estrutura**: Múltiplas conexões entre dispositivos
- **Vantagens**: Alta redundância e confiabilidade
- **Desvantagens**: Complexa e cara

## Modelo OSI (Open Systems Interconnection)

O modelo OSI é um padrão de referência que define como os sistemas de rede devem se comunicar.

### Camadas do Modelo OSI

1. **Física**: Transmissão de bits através do meio físico
2. **Enlace**: Controle de acesso ao meio e detecção de erros
3. **Rede**: Roteamento de pacotes entre redes diferentes
4. **Transporte**: Entrega confiável de dados fim a fim
5. **Sessão**: Estabelecimento e gerenciamento de sessões
6. **Apresentação**: Criptografia, compressão e formatação
7. **Aplicação**: Interface com aplicações do usuário

## Protocolos de Rede

### TCP/IP

#### TCP (Transmission Control Protocol)
- **Características**: Confiável, orientado à conexão
- **Uso**: Aplicações que requerem entrega garantida (HTTP, FTP, SSH)
- **Funcionalidades**: Controle de fluxo, detecção e correção de erros

#### UDP (User Datagram Protocol)
- **Características**: Não confiável, sem conexão
- **Uso**: Aplicações em tempo real (streaming, jogos, DNS)
- **Vantagens**: Menor overhead, maior velocidade

#### IP (Internet Protocol)
- **IPv4**: Endereços de 32 bits (ex: 192.168.1.1)
- **IPv6**: Endereços de 128 bits (ex: 2001:0db8:85a3::8a2e:0370:7334)
- **Função**: Roteamento de pacotes entre redes

### Protocolos de Aplicação

#### HTTP/HTTPS
- **HTTP**: Protocolo de transferência de hipertexto
- **HTTPS**: HTTP seguro com criptografia SSL/TLS
- **Porta**: 80 (HTTP), 443 (HTTPS)

#### FTP/SFTP
- **FTP**: Protocolo de transferência de arquivos
- **SFTP**: FTP seguro via SSH
- **Porta**: 21 (FTP), 22 (SFTP)

#### DNS (Domain Name System)
- **Função**: Tradução de nomes de domínio para endereços IP
- **Porta**: 53
- **Tipos de registro**: A, AAAA, CNAME, MX, NS

## Dispositivos de Rede

### Hub
- **Função**: Repetidor que conecta múltiplos dispositivos
- **Características**: Opera na camada física, domínio de colisão único
- **Status**: Obsoleto, substituído por switches

### Switch
- **Função**: Conecta dispositivos em uma LAN
- **Características**: Opera na camada de enlace, aprendizado de MAC
- **Vantagens**: Cada porta é um domínio de colisão separado

### Roteador
- **Função**: Conecta diferentes redes e roteia pacotes
- **Características**: Opera na camada de rede, tabela de roteamento
- **Protocolos**: RIP, OSPF, BGP

### Access Point (AP)
- **Função**: Fornece acesso wireless à rede
- **Padrões**: 802.11a/b/g/n/ac/ax (Wi-Fi 6)
- **Segurança**: WPA2, WPA3

## Endereçamento IP

### Classes de Endereços IPv4

#### Classe A
- **Faixa**: 1.0.0.0 a 126.255.255.255
- **Máscara**: 255.0.0.0 (/8)
- **Uso**: Grandes organizações

#### Classe B
- **Faixa**: 128.0.0.0 a 191.255.255.255
- **Máscara**: 255.255.0.0 (/16)
- **Uso**: Organizações médias

#### Classe C
- **Faixa**: 192.0.0.0 a 223.255.255.255
- **Máscara**: 255.255.255.0 (/24)
- **Uso**: Pequenas organizações

### Endereços Privados
- **10.0.0.0/8**: Classe A privada
- **172.16.0.0/12**: Classe B privada
- **192.168.0.0/16**: Classe C privada

### CIDR (Classless Inter-Domain Routing)
- **Conceito**: Notação que permite subnetting flexível
- **Formato**: Endereço/Prefixo (ex: 192.168.1.0/24)
- **Vantagem**: Uso mais eficiente do espaço de endereços

## Segurança de Redes

### Firewall
- **Função**: Controla tráfego baseado em regras de segurança
- **Tipos**: Packet filtering, stateful, application-layer
- **Implementação**: Hardware, software ou baseado em nuvem

### VPN (Virtual Private Network)
- **Função**: Cria túnel seguro através de rede pública
- **Protocolos**: OpenVPN, IPSec, L2TP, WireGuard
- **Uso**: Acesso remoto seguro, conexão entre filiais

### Criptografia
- **Simétrica**: Mesma chave para cifrar e decifrar (AES)
- **Assimétrica**: Par de chaves pública/privada (RSA)
- **Hash**: Função unidirecional para integridade (SHA-256)

## Troubleshooting de Rede

### Comandos Úteis

#### ping
```bash
ping google.com
# Testa conectividade com um host
```

#### traceroute
```bash
traceroute google.com
# Mostra o caminho que os pacotes percorrem
```

#### nslookup
```bash
nslookup google.com
# Consulta DNS para resolver nomes
```

#### netstat
```bash
netstat -an
# Mostra conexões de rede ativas
```

#### iptables (Linux)
```bash
iptables -L
# Lista regras do firewall
```

### Problemas Comuns

#### Conectividade
- **Sintomas**: Não consegue acessar sites ou serviços
- **Diagnóstico**: ping, traceroute, verificar configurações de IP
- **Soluções**: Verificar cabos, configurações de rede, DNS

#### Performance
- **Sintomas**: Lentidão na rede
- **Diagnóstico**: iperf, monitoramento de largura de banda
- **Soluções**: Otimizar configurações, upgrade de hardware

#### DNS
- **Sintomas**: Sites não carregam por nome, mas funcionam por IP
- **Diagnóstico**: nslookup, dig
- **Soluções**: Configurar DNS correto, limpar cache DNS

## Boas Práticas

### Documentação
- Manter diagramas de rede atualizados
- Documentar configurações e mudanças
- Inventário de dispositivos e endereços IP

### Monitoramento
- Implementar ferramentas de monitoramento (SNMP)
- Configurar alertas para problemas de rede
- Análise regular de logs

### Segurança
- Manter firmware/software atualizados
- Implementar segmentação de rede
- Backup regular de configurações
- Políticas de acesso restritivas

### Performance
- Planejamento de capacidade
- QoS (Quality of Service) para tráfego crítico
- Otimização de roteamento

## Recursos Complementares

### 📚 Referências e Documentação

#### Documentação Oficial
- [RFC 791 - Internet Protocol](https://tools.ietf.org/html/rfc791)
- [RFC 793 - Transmission Control Protocol](https://tools.ietf.org/html/rfc793)
- [RFC 1918 - Address Allocation for Private Internets](https://tools.ietf.org/html/rfc1918)
- [IEEE 802.11 Standards](https://standards.ieee.org/standard/802_11-2020.html)

#### Livros Recomendados
- **"Computer Networks" por Andrew Tanenbaum**
- **"TCP/IP Illustrated" por W. Richard Stevens**
- **"Network Security Essentials" por William Stallings**
- **"CCNA Routing and Switching" por Todd Lammle**

### 🎥 Conteúdo Audiovisual

#### Fundamentos
- [Introdução às Redes de Computadores - Conceitos Básicos](https://www.youtube.com/watch?v=jLYSmtDGF-k)
- [Modelo OSI e TCP/IP - Explicação Completa](https://www.youtube.com/watch?v=KOrWZnGbx7s)
- [Endereçamento IP e Subnetting](https://www.youtube.com/watch?v=G-m-iP1Ql6k)

#### Configuração e Administração
- [Configuração de Roteadores Cisco](https://www.youtube.com/watch?v=M_ICLwuP8NQ)
- [Switches: VLANs e Spanning Tree](https://www.youtube.com/watch?v=7kVemWNDUIo)
- [Configuração de Firewalls](https://www.youtube.com/watch?v=BZ4yuTQmxdo)

#### Segurança
- [VPNs: Implementação e Configuração](https://www.youtube.com/watch?v=OniiDXdwZJE)
- [Segurança em Redes Sem Fio](https://www.youtube.com/watch?v=RucNhKGR224)
- [Análise de Tráfego com Wireshark](https://www.youtube.com/watch?v=LdxqHDe9Dq4)

#### Tópicos Avançados
- [IPv6: Migração e Implementação](https://www.youtube.com/watch?v=u2RlU0KPJzU)
- [Software Defined Networks (SDN)](https://www.youtube.com/watch?v=Nh2hXUuKXyQ)
- [Monitoramento de Redes com SNMP](https://www.youtube.com/watch?v=PqgDoG4gLK0)

### 🛠️ Ferramentas Práticas

#### Simuladores de Rede
- **Cisco Packet Tracer**: Simulador oficial da Cisco
- **GNS3**: Emulador de redes avançado
- **EVE-NG**: Plataforma de emulação empresarial

#### Ferramentas de Monitoramento
- **Wireshark**: Análise de protocolos
- **Nmap**: Scanner de redes e portas
- **PRTG**: Monitoramento de infraestrutura
- **Nagios**: Sistema de monitoramento open source

#### Utilitários de Linha de Comando
- **ping**: Teste de conectividade
- **traceroute**: Rastreamento de rota
- **netstat**: Estatísticas de rede
- **ss**: Informações de socket (substituto do netstat)
- **iperf3**: Teste de largura de banda

### 🎯 Certificações Relevantes

#### Cisco
- **CCNA** (Cisco Certified Network Associate)
- **CCNP** (Cisco Certified Network Professional)
- **CCIE** (Cisco Certified Internetwork Expert)

#### CompTIA
- **Network+**: Fundamentos de redes
- **Security+**: Segurança em redes

#### Outras
- **CISSP**: Certified Information Systems Security Professional
- **CEH**: Certified Ethical Hacker
- **JNCIA**: Juniper Networks Certified Associate