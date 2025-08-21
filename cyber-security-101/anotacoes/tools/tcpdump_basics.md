# Tcpdump – The Basics

## Conceitos
- Captura de pacotes via CLI.
- Leve e útil em servidores Linux.

## Comandos
- Captura de todos os pacotes: `sudo tcpdump -i eth0`
- Captura com filtro: `sudo tcpdump -i eth0 port 80`
- Salvar captura: `sudo tcpdump -i eth0 -w capture.pcap`
- Ler captura: `tcpdump -r capture.pcap`

## Observações
- Complementa o Wireshark (análise via GUI).
- Essencial para pentesters que trabalham em servidores remotos.
