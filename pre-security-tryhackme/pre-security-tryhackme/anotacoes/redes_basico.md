# Redes – Fundamentos (TryHackMe Pre Security)

Anotações do módulo **Network Fundamentals**. Foco em entendimento prático para pentest.

---

## Visão geral
- **LAN vs WAN**: LAN = rede local (casa/empresa). WAN = interliga LANs (Internet).
- **Dispositivo final** (host), **switch** (camada 2), **roteador** (caminho entre redes, camada 3).

---

## Endereçamento IP e sub-redes
- **IPv4**: `A.B.C.D` (0–255).  
- **Privados**: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.  
- **CIDR**: `/24` = 255.255.255.0 (256 endereços); `/16` = 255.255.0.0.
- **Gateway padrão**: roteador que leva sua LAN para a Internet.
- **Máscara** define o tamanho da rede; hosts fora da mesma rede precisam do **gateway**.

---

## Protocolos de transporte (o que mais cai em pentest)
- **TCP** (orientado à conexão): handshake 3 vias (SYN, SYN/ACK, ACK), confiável. Ex.: HTTP/HTTPS, SSH.
- **UDP** (sem conexão): menor latência, sem garantia de entrega. Ex.: DNS, VoIP, jogos.
- **ICMP**: mensagens de controle (usado por `ping` e `traceroute`).

---

## Portas e serviços (decorar as mais comuns)
- **22** SSH · **80** HTTP · **443** HTTPS · **53** DNS · **25** SMTP · **110** POP3 · **143** IMAP · **3389** RDP · **445** SMB · **139** NetBIOS.
> Pentest: portas ajudam a inferir serviços/tecnologias e a priorizar vetores.

---

## Resolução de nomes (DNS)
- Transforma domínio → IP.
- **Registros**: `A` (IPv4), `AAAA` (IPv6), `CNAME` (alias), `MX` (email), `NS` (autoridade).
- Testes rápidos:
  - Linux: `dig tryhackme.com A +short`  
  - Windows: `nslookup tryhackme.com`

---

## Protocolos essenciais de camada 2/3
- **ARP**: mapeia IP ↔ MAC na LAN. Cache: `arp -a`.
- **DHCP**: distribui IP/máscara/gateway/DNS automaticamente (DORA: Discover, Offer, Request, Acknowledge).
- **NAT/PAT**: traduz IPs privados para um IP público (roteador). PAT = várias conexões → 1 IP (com portas).

---

## Ferramentas de diagnóstico
### Linux
```bash
ip a            # interfaces e IPs
ip route        # rotas e gateway
ping -c 4 1.1.1.1
traceroute tryhackme.com
dig tryhackme.com A +short
