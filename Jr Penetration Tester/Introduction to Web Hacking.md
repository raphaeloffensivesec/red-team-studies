# TryHackMe - Introdução ao Web Hacking  

## 📌 Room Information
- **Name:** Introduction to Web Hacking  
- **Difficulty:** Beginner  
- **Tags:** Web, OWASP Top 10, Exploitation, Pentesting Basics  

Este documento contém minhas anotações e aprendizados obtidos na room **Introduction to Web Hacking** do TryHackMe.  
A room apresenta, de forma prática, as vulnerabilidades web mais comuns que um pentester encontra no mundo real, acompanhadas de exemplos e exploração dentro de ambientes simulados.  

---

## 1. Walking an Application  
### 🔎 Conceito  
"Walking an application" significa navegar e mapear manualmente uma aplicação web para entender seu funcionamento antes de usar ferramentas automáticas.  

### 🛠 Técnicas utilizadas  
- Uso do **Inspector** do navegador (Chrome/Firefox DevTools).  
- Analisar **requisições e respostas HTTP**.  
- Observar parâmetros em URLs e formulários.  
- Descobrir rotas escondidas apenas explorando menus, botões e elementos do site.  

### 📖 Exemplo prático  
Ao inspecionar um formulário de login, descobri que os parâmetros de input são enviados em claro no corpo da requisição. Isso já indica a possibilidade de testar injeções.  

### 💡 Lição  
Muitas falhas são descobertas apenas **olhando com atenção** para como a aplicação responde ao usuário. O reconhecimento manual é a base de todo penteste web.  

---

## 2. Content Discovery  
### 🔎 Conceito  
Descobrir conteúdo escondido (diretórios, arquivos e endpoints) que não estão visíveis ao usuário.  

### 🛠 Técnicas utilizadas  
- Ferramentas de brute-force como:  
  - `dirb`  
  - `gobuster`  
- Arquivos comuns a verificar:  
  - `/robots.txt`  
  - `.git/`  
  - `.env`  
  - `backup.zip`  
- Testar diferentes extensões (`.php`, `.bak`, `.old`, `.txt`).  

### 📖 Exemplo prático  
Com `gobuster`, encontrei o endpoint `/admin` que não estava listado na interface do site, mas que permitia login administrativo.  

### 💡 Lição  
Administradores frequentemente deixam arquivos escondidos no servidor. Um atacante pode encontrar dados sensíveis e usá-los para escalonar privilégios.  

---

## 3. Subdomain Enumeration  
### 🔎 Conceito  
Subdomínios são como "mini-aplicações" dentro de um mesmo domínio. Cada um pode ter falhas próprias.  

### 🛠 Técnicas utilizadas  
- DNS bruteforce com `sublist3r`, `amass`, `assetfinder`.  
- Requisições DNS manuais com `nslookup`, `dig`.  
- Teste de *wildcards* para evitar falsos positivos.  

### 📖 Exemplo prático  
Descobri `test.dev.example.com` com um painel de staging rodando versão antiga do WordPress vulnerável a RCE.  

### 💡 Lição  
Subdomínios negligenciados são uma mina de ouro para pentesters. Muitas empresas esquecem ambientes de teste ou dev online.  

---

## 4. Authentication Bypass  
### 🔎 Conceito  
Quebrar ou contornar sistemas de autenticação.  

### 🛠 Técnicas utilizadas  
- Testar credenciais padrão (`admin:admin`).  
- Força bruta com `hydra` ou `Burp Intruder`.  
- Testar injeções em formulários (`' OR '1'='1`).  
- Manipulação de cookies ou tokens de sessão.  

### 📖 Exemplo prático  
O campo de login não sanitizava inputs, permitindo bypass com:  
```sql
' OR '1'='1' --
```  

### 💡 Lição  
Autenticação deve ser reforçada com: hashing seguro de senhas, MFA, validação no servidor.  

---

## 5. IDOR (Insecure Direct Object Reference)  
### 🔎 Conceito  
Ocorre quando um sistema usa identificadores previsíveis para acessar recursos e não verifica permissões.  

### 📖 Exemplo prático  
A URL `/profile?id=1` mostrava o perfil do usuário logado. Alterando para `/profile?id=2`, consegui acessar os dados de outro usuário.  

### 💡 Lição  
Autorização **nunca** deve ser feita apenas pelo cliente. Sempre deve ser validada no backend.  

---

## 6. File Inclusion  
### 🔎 Conceito  
Vulnerabilidades de inclusão de arquivos permitem carregar arquivos locais ou remotos no servidor.  

- **LFI (Local File Inclusion):** Leitura de arquivos locais (`/etc/passwd`).  
- **RFI (Remote File Inclusion):** Incluir arquivos externos maliciosos.  

### 📖 Exemplo prático  
Input vulnerável:  
```
page=../../../../etc/passwd
```  

### 💡 Lição  
Uma simples falta de validação em parâmetros pode levar a leitura de arquivos sensíveis ou até execução remota de código.  

---

## 7. SSRF (Server-Side Request Forgery)  
### 🔎 Conceito  
Forçar o servidor a realizar requisições que o atacante controla.  

### 🛠 Vetores  
- Fazer o servidor acessar serviços internos (`http://127.0.0.1:8080/admin`).  
- Explorar metadados de cloud (`http://169.254.169.254/latest/meta-data/`).  

### 💡 Lição  
SSRF é crítico em ambientes cloud, pois pode expor chaves de API e credenciais internas.  

---

## 8. XSS (Cross-Site Scripting)  
### 🔎 Conceito  
Permite injetar código JavaScript malicioso em páginas web.  

### Tipos  
- **Refletido:** script aparece na resposta imediatamente.  
- **Armazenado:** script é salvo no banco de dados e executado para outros usuários.  

### 📖 Exemplo prático  
Comentário injetado:  
```html
<script>alert('XSS')</script>
```  

### 💡 Lição  
XSS permite roubo de cookies, manipulação do DOM e ataques de phishing avançados.  

---

## 9. Race Conditions  
### 🔎 Conceito  
Exploração de falhas lógicas quando várias requisições ocorrem ao mesmo tempo.  

### 📖 Exemplo prático  
Sistema de transferência bancária não bloqueava múltiplas requisições. Enviando 100 requisições simultâneas, o saldo era debitado apenas uma vez, mas o crédito era aplicado várias vezes.  

### 💡 Lição  
Condições de corrida são difíceis de detectar, mas podem causar enormes prejuízos financeiros.  

---

## 10. Command Injection  
### 🔎 Conceito  
Quando a entrada do usuário é usada diretamente em comandos do sistema operacional.  

### 📖 Exemplo prático  
Formulário de ping vulnerável:  
```
ping -c 1 [input]
```
Se o input for:  
```
127.0.0.1; whoami
```
O comando `whoami` será executado no servidor.  

### 💡 Lição  
Todo input deve ser validado e, se possível, nunca enviado direto para funções de execução do sistema.  

---

## 11. SQL Injection  
### 🔎 Conceito  
Manipulação de queries SQL injetando código malicioso.  

### 🛠 Técnicas  
- Login bypass:  
```sql
' OR '1'='1' --
```  
- Dump de dados com `UNION SELECT`.  
- Ferramenta de automação: `sqlmap`.  

### 💡 Lição  
SQL Injection pode levar à total tomada de controle do banco de dados, expondo informações confidenciais.  

---

## 📝 Lessons Learned  
- O OWASP Top 10 continua sendo a **base fundamental** para pentesters web.  
- Muitas falhas não precisam de ferramentas sofisticadas — **observar e testar manualmente** já revela muito.  
- Segurança web depende de **validação e sanitização de input**.  
- Nunca confiar no cliente, sempre validar e filtrar no servidor.  

---

## ⚠️ Disclaimer  
Este conteúdo é **apenas para fins educacionais**.  
Nunca utilize estas técnicas fora de ambientes controlados, como laboratórios e plataformas legais (TryHackMe, HackTheBox, etc).  

