# 📘 Cybersecurity 101 – Security Solutions Notes

Este documento reúne minhas anotações sobre os principais **Security Solutions** estudados no módulo **Cybersecurity 101**.  
Organizado de forma clara, para posterior consulta e estudo contínuo.

---

## 🔹 1. Introduction to SIEM
### ✅ O que é SIEM (Security Information and Event Management)
- **SIEM** combina **coleta, correlação, monitoramento e análise** de eventos de segurança.
- Centraliza logs de:
  - Firewalls
  - Servidores
  - IDS/IPS
  - Aplicações críticas
- Permite **detecção de ameaças em tempo real** e **resposta a incidentes**.

### 📊 Funcionalidades principais
1. **Coleta e agregação de logs** → unifica dados de diferentes dispositivos.
2. **Correlação de eventos** → identifica padrões suspeitos.
3. **Alertas automáticos** → gera notificações em tempo real.
4. **Dashboards e relatórios** → visibilidade clara do ambiente.
5. **Investigação forense** → armazenamento histórico de eventos.

### 🛠 Exemplos de SIEM
- Splunk
- IBM QRadar
- Elastic SIEM
- Azure Sentinel

---

## 🔹 2. Firewall Fundamentals
### ✅ O que é um Firewall
- Dispositivo ou software que controla **tráfego de rede** com base em regras pré-definidas.
- Atua como **primeira barreira** entre rede interna e externa.

### 🔑 Tipos de Firewall
1. **Packet Filtering Firewall**
   - Analisa pacotes com base em **IP, porta e protocolo**.
   - Rápido, mas básico.
2. **Stateful Inspection**
   - Mantém o **estado da conexão**.
   - Mais seguro que packet filtering.
3. **Application Layer Firewall (Proxy)**
   - Inspeciona o tráfego em **nível de aplicação**.
   - Pode bloquear requisições HTTP, FTP, etc.
4. **Next-Generation Firewall (NGFW)**
   - Combina firewall tradicional com:
     - IDS/IPS
     - Filtragem avançada
     - Controle de aplicações

### 🔐 Funções principais
- Prevenção de acessos não autorizados.
- Segmentação de rede.
- Definição de regras de entrada e saída.

---

## 🔹 3. IDS Fundamentals
### ✅ O que é IDS (Intrusion Detection System)
- Sistema que **monitora tráfego de rede** ou atividades em hosts.
- Objetivo: **detectar possíveis intrusões**.

### 📊 Tipos de IDS
1. **NIDS (Network-based IDS)**
   - Analisa tráfego em tempo real.
   - Detecta ataques de rede (scan, DoS, exploits).
2. **HIDS (Host-based IDS)**
   - Instalado em máquinas específicas.
   - Monitora arquivos de sistema, logs, integridade.

### ⚙️ Métodos de Detecção
- **Assinaturas (Signature-based)** → compara com base conhecida de ataques.
- **Anomalias (Anomaly-based)** → identifica desvios de comportamento normal.

### 🛠 Exemplos de IDS
- Snort
- Suricata
- OSSEC

---

## 🔹 4. Vulnerability Scanner Overview
### ✅ O que é um Vulnerability Scanner
- Ferramenta que **analisa sistemas e redes** em busca de falhas de segurança.
- **Identifica vulnerabilidades** antes que sejam exploradas.

### 📊 Funções principais
- **Mapeamento da rede**.
- **Identificação de serviços e versões**.
- **Detecção de vulnerabilidades conhecidas** (CVEs).
- **Relatórios de risco** com recomendações de correção.

### 🛠 Exemplos de Scanners
- Nessus
- OpenVAS
- Qualys
- Nexpose

### 🔑 Diferença para Pentest
- **Scanner**: identifica falhas automaticamente.
- **Pentest**: envolve exploração manual para validar riscos.
