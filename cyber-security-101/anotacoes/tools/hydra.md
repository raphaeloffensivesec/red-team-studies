# Hydra 🐉

## 📌 O que é o Hydra?
- O **THC-Hydra** é uma ferramenta rápida e poderosa para ataques de força bruta em serviços de rede.
- Suporta diversos protocolos: **SSH, FTP, HTTP, SMB, Telnet, RDP, VNC**, entre outros.
- Muito utilizado em **testes de penetração** para identificar credenciais fracas.

---

## ⚙️ Sintaxe básica
hydra [opções] <alvo> <serviço>

Exemplo:
hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.0.10 ssh

---

## 🔑 Principais opções
- `-l <usuário>` → define um único usuário
- `-L <arquivo>` → lista de usuários
- `-p <senha>` → define uma única senha
- `-P <arquivo>` → lista de senhas (wordlist)
- `-s <porta>` → especifica porta (caso não seja a padrão)
- `-t <n>` → número de threads (paralelismo)
- `-V` → modo verboso (mostra cada tentativa)
- `-f` → para ao encontrar a primeira credencial válida
- `-o <arquivo>` → salva resultados

---

## 🚀 Exemplos práticos

### 1. SSH brute force
hydra -l root -P rockyou.txt 192.168.0.10 ssh  
➡️ Tenta autenticar no SSH do alvo com usuário **root**.

---

### 2. FTP com lista de usuários e senhas
hydra -L users.txt -P passwords.txt ftp://192.168.0.15

---

### 3. HTTP POST form (login web)
hydra -l admin -P rockyou.txt 192.168.0.20 http-post-form "/login:username=^USER^&password=^PASS^:F=Login Failed"

- `^USER^` → substituído pelo usuário  
- `^PASS^` → substituído pela senha  
- `F=Login Failed` → mensagem que identifica falha no login

---

### 4. RDP (Remote Desktop Protocol)
hydra -t 4 -V -f -L users.txt -P pass.txt rdp://192.168.0.30

---

## ⚠️ Boas práticas e observações
- Use **somente em ambientes autorizados** (lab, CTF, pentest autorizado).  
- Combine com wordlists realistas (ex.: **rockyou.txt**, **seclists**).  
- Ajuste as **threads (-t)** para não causar negação de serviço.  
- Se possível, use junto com outras ferramentas para reconhecimento (ex.: **Nmap**, **BurpSuite**).  
