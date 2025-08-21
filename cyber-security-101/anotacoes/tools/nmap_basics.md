# Nmap – The Basics

## Conceitos
- Ferramenta de varredura de rede e host discovery.
- Detecta portas abertas, serviços, sistemas operacionais.

## Comandos
- Varredura simples: `nmap 192.168.1.10`
- Varredura completa: `nmap -A 192.168.1.10`
- Varredura de portas específicas: `nmap -p 22,80,443 192.168.1.10`
- Descoberta de hosts ativos: `nmap -sn 192.168.1.0/24`

## Observações
- Muito usada em pentesting.
- Fornece informações valiosas sobre serviços e vulnerabilidades.
