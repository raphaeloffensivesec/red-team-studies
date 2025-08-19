# HTTP – Fundamentos da Web

## Conceitos
- **HTTP (HyperText Transfer Protocol):** protocolo de comunicação entre cliente (browser) e servidor.
- **HTTPS:** HTTP + TLS (criptografia, porta 443).
- **Método de requisição:** define o que o cliente quer do servidor.
  - `GET` → solicita recurso.
  - `POST` → envia dados (ex.: formulário).
  - `PUT` → atualiza recurso.
  - `DELETE` → remove recurso.
- **Status Codes (resposta do servidor):**
  - `1xx` → Informativo
  - `2xx` → Sucesso (200 OK, 201 Created)
  - `3xx` → Redirecionamento (301 Moved Permanently, 302 Found)
  - `4xx` → Erro do cliente (400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found)
  - `5xx` → Erro do servidor (500 Internal Server Error)
- **Headers (cabeçalhos):**
  - **De requisição (cliente → servidor):**
    - `User-Agent`: navegador usado
    - `Host`: domínio solicitado
    - `Cookie`: dados de sessão
  - **De resposta (servidor → cliente):**
    - `Set-Cookie`: cria cookie no cliente
    - `Content-Type`: tipo de conteúdo (HTML, JSON, imagem)
    - `Server`: tecnologia usada no backend
- **Body:** parte da requisição/resposta que carrega dados (HTML, JSON, etc.).

## Ferramentas úteis
- **curl** (linha de comando) → testar requisições HTTP.
- **DevTools do navegador (F12 → Network)** → inspecionar requests/responses.
- **Burp Suite** → interceptar e manipular tráfego web.
