# Defensive Security Tooling

Este documento reúne minhas anotações sobre as principais ferramentas de **Defensive Security** estudadas no módulo **Defensive Security Tooling**.

---

## 1. CyberChef: The Basics

### O que é
- Ferramenta open-source desenvolvida pela GCHQ (inteligência britânica).
- Conhecida como “Swiss Army Knife for Data”.
- Funciona diretamente no navegador (online ou offline).
- Interface gráfica com suporte a **pipelines de operações**.

### Funcionalidades principais
- **Conversões**: Base64, Hex, ASCII, URL encoding/decoding.
- **Criptografia e Hashing**: AES, DES, RC4, MD5, SHA1, SHA256, etc.
- **Compressão e Descompressão**: Gzip, Bzip2, Base85, etc.
- **Análise forense**: extração de strings, detecção de headers de arquivos.
- **Regex**: busca, substituição e manipulação de dados textuais.
- **Visualização**: conversão de bytes em imagens, tabelas, JSON, etc.

### Casos de uso
1. Decodificação de payloads em **Base64**.
2. Extração de dados escondidos em imagens ou binários.
3. Construção de pipelines automáticos de conversão + compressão + decodificação.
4. Manipulação rápida de malware scripts ofuscados.

### Exemplo prático
- Receber um payload em **Base64**:
  - Input: string codificada.
  - Operações: `From Base64` → `Render Image`.
  - Output: exibe imagem embutida.

- Pipeline útil:
  - `From Hex` → `Gunzip` → `Strings`  
  - Permite analisar binários comprimidos e extrair conteúdo legível.

### Instalação / Uso
- Versão online: [CyberChef Online](https://gchq.github.io/CyberChef)
- Versão local (para OPSEC):  
  - Baixar release do GitHub e abrir `index.html` no navegador.

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
