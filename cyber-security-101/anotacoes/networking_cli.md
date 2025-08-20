# 🌐 Networking – Cyber Security 101

## 📖 Introdução
Rede (networking) é a base de toda comunicação entre computadores.  
Entender como dispositivos se conectam, trocam dados e quais protocolos estão envolvidos é fundamental em **cibersegurança**.  
Nesta seção, estudei os principais conceitos e comandos práticos de **Windows** e **Linux** para diagnosticar e entender redes.

---

## 📌 Conceitos Fundamentais

### 🔹 Endereços IP
- **IPv4**: 32 bits, formato decimal (ex.: `192.168.1.10`)
- **IPv6**: 128 bits, formato hexadecimal (ex.: `2001:0db8:85a3::8a2e:0370:7334`)
- **Máscara de Sub-rede**: define a parte da rede e do host (ex.: `255.255.255.0`).
- **Gateway Padrão**: saída da rede local para a internet.

### 🔹 Protocolos de Transporte
- **TCP**: orientado à conexão, confiável (ex.: HTTP, FTP, SSH).
- **UDP**: sem conexão, mais rápido, mas não garante entrega (ex.: DNS, VoIP).

### 🔹 Portas
- **0–1023**: portas conhecidas (HTTP: 80, HTTPS: 443, SSH: 22).
- **1024–49151**: portas registradas.
- **49152–65535**: portas dinâmicas/efêmeras.

### 🔹 Protocolos de Rede Importantes
- **ICMP** → diagnóstico de rede (`ping`, `traceroute`).
- **DNS** → tradução de nomes para IPs.
- **DHCP** → atribuição automática de IPs.
- **ARP** → resolve IP → endereço MAC.
- **NAT** → traduz endereços internos em um IP público.

---

## 🖥️ Networking no Windows – Comandos Práticos

- `ipconfig /all` → mostra IP, máscara, gateway, DNS.
- `ping google.com` → testa conectividade com um host.
- `tracert google.com` → mostra a rota até o destino.
- `nslookup google.com` → consulta DNS para resolver nomes.
- `netstat -ano` → lista conexões de rede ativas e portas em escuta.
- `arp -a` → tabela ARP, mapeando IPs ↔ MACs.

---

## 🐧 Networking no Linux – Comandos Práticos

- `ifconfig` ou `ip a` → mostra interfaces e endereços.
- `ping -c 4 8.8.8.8` → envia pacotes ICMP.
- `traceroute google.com` → rota até o destino.
- `dig google.com` → consulta DNS detalhada.
- `netstat -tulnp` ou `ss -tulnp` → lista portas abertas e processos associados.
- `arp -n` → tabela ARP.
- `nc -lvp 4444` → abre uma porta com Netcat.
- `nc <IP> <porta>` → conecta em um serviço remoto.

---

## 🔧 Ferramentas de Rede

- **Wireshark** → captura e análise de pacotes.
- **Tcpdump** → versão CLI para captura de tráfego no Linux.
- **Netcat (nc)** → "canivete suíço" para conexões TCP/UDP.
- **Nmap** → varredura de hosts e portas (básico para pentesting).
- **Curl** → testes HTTP/HTTPS via terminal.

---

## ⚡ Diagnóstico de Rede – Passo a Passo

1. **Verificar configuração de rede**  
   - Windows: `ipconfig /all`  
   - Linux: `ip a`
2. **Testar conectividade básica**  
   - `ping 8.8.8.8` (Google DNS).
3. **Testar resolução DNS**  
   - `nslookup openai.com` (Windows)  
   - `dig openai.com` (Linux)
4. **Ver rota até o destino**  
   - `tracert` (Windows)  
   - `traceroute` (Linux)
5. **Checar conexões ativas**  
   - `netstat -ano` (Windows)  
   - `ss -tulnp` (Linux)

---

## 🛡️ Networking e Segurança

- **Portas abertas** são potenciais pontos de ataque → monitorar com `netstat` ou `nmap`.
- **DNS Spoofing** pode redirecionar tráfego malicioso → validar resoluções.
- **Sniffing** (ex.: Wireshark) pode capturar credenciais se tráfego não for criptografado.
- **Firewalls** controlam entrada/saída de tráfego.
- **VPNs** protegem comunicações com criptografia.

---

## 📊 Conclusão
O módulo de Networking reforçou que **segurança começa na rede**.  
Dominar protocolos, portas e comandos de diagnóstico é essencial para avançar em pentesting, análise forense ou defesa cibernética.

