# HTTP – Fundamentos da Web

## 🔹 1. O que é HTTP?
- **HTTP (HyperText Transfer Protocol):** protocolo de comunicação entre **cliente** (ex.: navegador) e **servidor web**.
- Trabalha no **modelo request/response** (requisição/resposta).
- Funciona sobre o **TCP** (porta 80 → HTTP, porta 443 → HTTPS).
- É **stateless** (não guarda estado entre requisições). Para manter estado, usa **cookies, sessões e tokens**.

---

## 🔹 2. Ciclo de funcionamento
1. Cliente envia **request** (requisição):
   - Linha de requisição (método, caminho e versão).
   - Headers (metadados).
   - Body (opcional, usado em POST, PUT, etc.).
2. Servidor processa e responde com **response**:
   - Status code.
   - Headers de resposta.
   - Body (HTML, JSON, imagem, etc.).

---

## 🔹 3. Estrutura de uma requisição
Exemplo (GET):
```
GET /index.html HTTP/1.1
Host: www.exemplo.com
User-Agent: Mozilla/5.0
Accept: text/html
Cookie: sessionid=12345
```

Exemplo (POST):
```
POST /login HTTP/1.1
Host: www.exemplo.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

usuario=admin&senha=1234
```

---

## 🔹 4. Métodos HTTP mais comuns
- **GET:** busca recurso no servidor (idempotente → não altera dados).
- **POST:** envia dados ao servidor (ex.: formulários).
- **PUT:** cria ou substitui um recurso existente.
- **PATCH:** altera parcialmente um recurso.
- **DELETE:** remove recurso.
- **HEAD:** retorna apenas headers (sem body).
- **OPTIONS:** mostra métodos suportados pelo servidor (ex.: usado em CORS).
- **TRACE:** retorna a requisição recebida (quase não usado, pode ser risco de segurança).

---

## 🔹 5. Status Codes
### ✅ Sucesso
- `200 OK` → resposta padrão de sucesso.
- `201 Created` → recurso criado.
- `204 No Content` → sucesso, sem conteúdo.

### 🔄 Redirecionamento
- `301 Moved Permanently` → redirecionamento fixo.
- `302 Found` → redirecionamento temporário.
- `307 Temporary Redirect` → redirecionamento mantendo método.

### ⚠ Erros do cliente
- `400 Bad Request` → requisição malformada.
- `401 Unauthorized` → precisa autenticação.
- `403 Forbidden` → acesso proibido mesmo autenticado.
- `404 Not Found` → recurso não encontrado.
- `405 Method Not Allowed` → método não permitido.
- `429 Too Many Requests` → limite de requisições atingido.

### ❌ Erros do servidor
- `500 Internal Server Error` → erro genérico.
- `502 Bad Gateway` → problema entre servidores.
- `503 Service Unavailable` → servidor fora do ar/ocupado.
- `504 Gateway Timeout` → tempo de resposta excedido.

---

## 🔹 6. Headers principais
### Requisição (client → server)
- `Host`: domínio solicitado.
- `User-Agent`: navegador ou cliente usado.
- `Accept`: tipos de resposta aceitos (`text/html`, `application/json`).
- `Authorization`: credenciais (Basic, Bearer token, etc).
- `Cookie`: envia cookies salvos.

### Resposta (server → client)
- `Content-Type`: formato do corpo (HTML, JSON, imagem).
- `Content-Length`: tamanho em bytes.
- `Set-Cookie`: cria cookie no cliente.
- `Server`: tecnologia do servidor (ex.: nginx, Apache).
- `Location`: usado em redirecionamentos.

---

## 🔹 7. Cookies e Sessões
- **Cookies:** armazenados no navegador; usados para autenticação, preferências, rastreamento.
- **Sessões:** criadas no servidor, identificadas por um cookie (ex.: `PHPSESSID`, `JSESSIONID`).
- **Segurança:**
  - `HttpOnly`: previne acesso via JavaScript.
  - `Secure`: só enviado em HTTPS.
  - `SameSite`: previne ataques CSRF.

---

## 🔹 8. HTTPS
- É o **HTTP + TLS (SSL)**.
- Criptografa comunicação entre cliente e servidor.
- Evita sniffing (captura de tráfego) e MITM (Man-in-the-Middle).
- Porta padrão: **443**.

---

## 🔹 9. Ferramentas práticas
- **curl:** linha de comando para requisições HTTP.
- **wget:** baixar páginas/arquivos via HTTP.
- **Netcat (nc):** simular conexões TCP e enviar requests manualmente.
- **Burp Suite / OWASP ZAP:** proxy para interceptar/modificar tráfego.
- **Navegador (DevTools – F12):** inspecionar requests/responses.

---

## 🔹 10. Exemplos práticos
### Testar requisição GET
```bash
curl -v http://example.com
```

### Testar requisição POST
```bash
curl -X POST -d "usuario=admin&senha=123" http://example.com/login
```

### Ver apenas headers
```bash
curl -I http://example.com
```

### Testar diferentes status codes
```bash
curl -i http://httpstat.us/404
curl -i http://httpstat.us/500
```

---

## 🔹 11. HTTP em Segurança
- Requisições malformadas → podem causar falhas (ex.: **HTTP Request Smuggling**).
- Manipulação de headers → explorar autenticação ou bypass de restrições.
- Testar autenticação → brute force em login.
- Cookies inseguros → session hijacking.
- Status codes → ajudam a mapear segurança do site (ex.: 403, 401, 500 em fuzzing).
