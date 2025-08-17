# Redes – Fundamentos (TryHackMe Pre Security)

Este documento reúne minhas anotações do módulo **Network Fundamentals** do TryHackMe (Pre Security Path).  
O objetivo é consolidar os **conceitos essenciais de redes** que todo profissional de cibersegurança precisa dominar.

---

## 1. Conceitos básicos de redes
- **Rede**: conjunto de dispositivos interligados para compartilhar dados.
- **LAN (Local Area Network)**: rede local, geralmente dentro de casa, escola ou empresa.
- **WAN (Wide Area Network)**: conecta redes locais distantes, exemplo: a Internet.
- **Endereço IP**: número que identifica cada dispositivo em uma rede.
  - IPv4: formato `x.x.x.x` (ex.: `192.168.0.1`).
  - IPv6: formato hexadecimal, mais longo (ex.: `2001:0db8::1`).
- **Endereço privado**: usado em redes internas, não é acessível diretamente da internet.
  - Faixas comuns: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.
- **Gateway**: o “roteador de saída” que conecta a rede local à internet.
- **DNS (Domain Name System)**: traduz nomes de domínio (`tryhackme.com`) para endereços IP.

---

## 2. Protocolos importantes
- **TCP (Transmission Control Protocol)**  
  - Conexão orientada, garante entrega confiável.  
  - Usado em: HTTP/HTTPS, SSH, FTP.  

- **UDP (User Datagram Protocol)**  
  - Não garante entrega, mas é mais rápido.  
  - Usado em: streaming, jogos online, VoIP.  

- **ICMP (Internet Control Message Protocol)**  
  - Usado por ferramentas como `ping` e `traceroute`.  

---

## 3. Portas e serviços
- Cada serviço na rede “ouve” em uma porta lógica. Exemplos:
  - **22** → SSH  
  - **80** → HTTP  
  - **443** → HTTPS  
  - **53** → DNS  
  - **3389** → RDP (Remote Desktop)  

Saber essas portas de cor é essencial para pentesting.

---

## 4. Ferramentas de diagnóstico
### Linux
```bash
# Mostrar interfaces de rede
ip a

# Mostrar rotas
ip route

# Testar conectividade
ping -c 4 1.1.1.1

# Ver caminho até um destino
traceroute tryhackme.com

# Consultar DNS
dig tryhackme.com

### Windows

# Mostrar interfaces
ipconfig /all

# Testar conectividade
ping 1.1.1.1

# Ver caminho até o destino
tracert tryhackme.com

# Consultar DNS
nslookup tryhackme.com
