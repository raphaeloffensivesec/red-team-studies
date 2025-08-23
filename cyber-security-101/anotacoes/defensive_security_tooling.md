# Defensive Security Tooling

Este documento reúne minhas anotações sobre as principais ferramentas de **Defensive Security** estudadas no módulo **Defensive Security Tooling**.

---

## 1. CyberChef: The Basics
### O que é
- Ferramenta web interativa chamada de "Swiss Army Knife for Data".
- Utilizada para análise e transformação de dados.
- Interface baseada em drag-and-drop de operações.

### Funcionalidades principais
- Conversões de codificação (Base64, Hex, ASCII).
- Operações criptográficas (hashes, ciphers).
- Análise forense (extração de strings, decodificação de payloads).
- Manipulação de dados em formato binário, texto e JSON.

### Casos de uso
- Decodificar cargas de malware.
- Converter entre formatos durante análise.
- Auxiliar em engenharia reversa.

---

## 2. CAPA: The Basics
### O que é
- Ferramenta de análise estática criada pela FireEye/Mandiant.
- Identifica **capacidades** em binários (o que o programa é capaz de fazer).

### Funcionalidades principais
- Detecta comportamentos maliciosos em executáveis.
- Baseada em regras YARA e lógica de matching.
- Trabalha em nível de funções do binário.

### Casos de uso
- Determinar rapidamente o que um malware pode realizar (ex.: keylogging, comunicação em rede, persistência).
- Priorizar análises em grandes coleções de amostras.

---

## 3. REMnux: Getting Started
### O que é
- Distribuição Linux focada em **malware analysis**.
- Contém conjunto de ferramentas para análise estática e dinâmica.

### Funcionalidades principais
- Ferramentas para engenharia reversa.
- Descompiladores e disassemblers.
- Análise de rede e manipulação de tráfego.
- Utilitários de decodificação.

### Casos de uso
- Criação de ambiente controlado para analisar malware.
- Realizar análise de tráfego suspeito.
- Automatizar tarefas de engenharia reversa.

---

## 4. FlareVM: Arsenal of Tools
### O que é
- Ambiente Windows customizado para análise de malware.
- Criado pela FireEye.
- Fornece um arsenal de ferramentas para engenharia reversa e análise forense.

### Funcionalidades principais
- Disassemblers (IDA Free, radare2).
- Debuggers (x64dbg, OllyDbg).
- Ferramentas para análise de documentos maliciosos.
- Integração com utilitários de rede e exploração.

### Casos de uso
- Analisar malware que depende de Windows APIs.
- Depuração de binários em ambiente Windows.
- Testar comportamento dinâmico de samples.
