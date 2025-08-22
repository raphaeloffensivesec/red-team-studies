# Web Hacking – TryHackMe Cybersecurity 101

## 1. Fundamentos da Web
- A web funciona com base no modelo **cliente-servidor**:
  - **Cliente (browser)** → faz requisições HTTP/HTTPS.
  - **Servidor (web server)** → responde com recursos (HTML, JSON, imagens, etc.).
- Protocolos principais:
  - **HTTP (HyperText Transfer Protocol)** – comunicação em texto puro.
  - **HTTPS (HTTP Secure)** – usa TLS/SSL para encriptação.
- Estrutura de uma URL:
  - `https://example.com/login?user=admin`
    - **https** → protocolo
    - **example.com** → domínio
    - **/login** → rota/recurso
    - **?user=admin** → parâmetro de consulta
- Códigos de resposta comuns:
  - `200 OK` → sucesso
  - `301 Moved Permanently` → redirecionamento
  - `401 Unauthorized` → não autenticado
  - `403 Forbidden` → acesso negado
  - `404 Not Found` → recurso não encontrado
  - `500 Internal Server Error` → erro no servidor

---

## 2. Métodos HTTP
- **GET** – solicita dados (parâmetros visíveis na URL).  
- **POST** – envia dados no corpo da requisição.  
- **PUT** – atualiza recursos existentes.  
- **DELETE** – remove recursos.  
- **HEAD** – igual ao GET, mas sem corpo de resposta (útil para checagem).  
- **OPTIONS** – mostra métodos permitidos em um recurso.  

---

## 3. Cabeçalhos HTTP
Exemplos importantes:
- `Host` – domínio do servidor.  
- `User-Agent` – identifica navegador/cliente.  
- `Cookie` – armazena dados de sessão.  
- `Authorization` – autenticação básica, bearer token, JWT.  
- `Referer` – mostra a origem da requisição.  

Esses cabeçalhos podem ser manipulados em ataques.  

---

## 4. JavaScript Essentials
- Linguagem **client-side**, executada no navegador.  
- Usada para:
  - Manipular o **DOM** (Document Object Model).  
  - Enviar requisições assíncronas (**AJAX, Fetch API**).  
  - Validar dados antes de enviar para o servidor.  

⚠️ **Riscos de segurança**:
- **XSS (Cross-Site Scripting)** – injeção de scripts maliciosos.  
  - Exemplo:  
    ```html
    <script>alert('XSS!')</script>
    ```
- **DOM-based XSS** – manipulação direta do DOM sem validação.  
- **Input validation** → validação no cliente não substitui validação no servidor.  

Ferramentas úteis:
- Console do navegador (F12).  
- Extensões de devtools para analisar o fluxo de dados.  

---

## 5. SQL Fundamentals
- **SQL (Structured Query Language)** gerencia dados em bancos relacionais.  
- Principais comandos:
  - `SELECT * FROM users;`
  - `INSERT INTO users (username, password) VALUES ('admin', '1234');`
  - `UPDATE users SET password='nova' WHERE id=1;`
  - `DELETE FROM users WHERE id=5;`

### SQL Injection (SQLi)
- Exploração de falhas em consultas SQL mal sanitizadas.  
- Exemplo vulnerável:
  ```sql
  SELECT * FROM users WHERE username = '$input';
Se $input = ' OR '1'='1 → bypass de autenticação.

## Técnicas:
- **Union-based** – extrair dados usando UNION.
- **Boolean-based blind** – inferir resultados por true/false.
- **Time-based blind** – usar funções como SLEEP() para extrair informações lentamente.

## Proteções:
- Prepared statements (consultas parametrizadas).
- Sanitização e escaping de entradas.
- Least privilege no banco.

## 6. OWASP Top 10 (2021)

Lista das 10 vulnerabilidades mais críticas em aplicações web:
- **Broken Access Control** – falhas em permissões e acessos.
- **Cryptographic Failures** – senhas salvas sem hash, TLS fraco, etc.
- **Injection** – SQLi, NoSQLi, OS command injection.
- **Insecure Design** – arquitetura fraca e lógica de negócios vulnerável.
- **Security Misconfiguration** – erros em servidores, frameworks, permissões.
- **Vulnerable and Outdated Components** – bibliotecas antigas, sem patch.
- **Identification and Authentication Failures** – falhas em login e sessão.
- **Software and Data Integrity Failures** – problemas com pipelines, supply chain.
- **Security Logging and Monitoring Failures** – falta de logs e monitoramento.
- **Server-Side Request Forgery (SSRF)** – servidor usado para fazer requisições não autorizadas.
