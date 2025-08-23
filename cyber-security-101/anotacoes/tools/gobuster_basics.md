# Gobuster 🚀

## 📌 O que é o Gobuster?
- Ferramenta de **força bruta e enumeração** escrita em Go.
- Utilizada principalmente para:
  - Descoberta de **diretórios e arquivos escondidos** em servidores web.
  - Enumeração de **subdomínios**.
- Muito rápido, pois usa **Go routines (multithreading)**.

---

## ⚙️ Sintaxe básica
gobuster [modo] [opções]

Exemplo:
gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt

---

## 🔑 Principais modos
- `dir` → Enumeração de diretórios/arquivos em um site.
- `dns` → Enumeração de subdomínios.
- `vhost` → Enumeração de virtual hosts.

---

## 🔑 Principais opções
- `-u <URL>` → Define a URL alvo.
- `-w <wordlist>` → Especifica a wordlist de diretórios, arquivos ou subdomínios.
- `-t <threads>` → Número de threads (padrão: 10).
- `-x <extensões>` → Lista de extensões para testar (ex: `.php,.html,.txt`).
- `-s <códigos>` → Códigos HTTP a mostrar (ex.: `200,204,301,302,403`).
- `-k` → Ignorar certificados SSL inválidos.
- `-o <arquivo>` → Salvar resultados em arquivo.
- `-q` → Modo quiet (oculta banners e resultados irrelevantes).

---

## 🚀 Exemplos práticos

### 1. Descobrir diretórios
gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt

---

### 2. Descobrir arquivos com extensão específica
gobuster dir -u http://example.com -w wordlist.txt -x php,html,txt

---

### 3. Descobrir subdomínios
gobuster dns -d example.com -w /usr/share/wordlists/subdomains.txt

---

### 4. Virtual Host enumeration
gobuster vhost -u http://example.com -w /usr/share/wordlists/vhosts.txt

---

### 5. Filtrando por códigos de status
gobuster dir -u http://example.com -w wordlist.txt -s 200,301,403

---

## ⚠️ Boas práticas e observações
- Use wordlists adequadas (ex.: **SecLists**).
- Combine com ferramentas como **BurpSuite** e **Nmap** para uma enumeração mais completa.
- Ajuste threads `-t` para evitar sobrecarregar o servidor.
- Ideal para **pentests web**, CTFs e **bug bounty**.

