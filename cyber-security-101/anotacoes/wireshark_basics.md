# Wireshark – The Basics

## Conceitos
- Ferramenta de captura e análise de pacotes.
- Permite filtrar, inspecionar protocolos e identificar problemas de rede.

## Comandos / Operações
- Capturar pacotes de uma interface.
- Filtros de visualização:
  - `ip.addr == 192.168.1.10`
  - `tcp.port == 80`
  - `http.request`
- Seguir streams TCP/UDP.
- Exportar pacotes para arquivo `.pcap` para análise posterior.

## Observações
- Muito útil para troubleshooting e análise de tráfego suspeito.
- Fundamental para entender protocolos em prática.
