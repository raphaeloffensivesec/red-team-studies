# Burp Suite – Tools

## 1. O que é o Burp Suite?
- Ferramenta **all-in-one** para **testes de segurança em aplicações web**.
- Desenvolvido pela **PortSwigger**.
- Usado por **pentesters, bug hunters e equipes de Red Team**.
- Atua como **proxy interceptador** entre o navegador e o servidor web.

---

## 2. Estrutura e Componentes Principais

### 🔹 Proxy
- Intercepta o tráfego entre **navegador ↔ servidor**.
- Permite modificar **requisições e respostas** em tempo real.
- Usado para testes de **manipulação de parâmetros** e **cookies**.

### 🔹 Repeater
- Envia requisições manualmente várias vezes.
- Ideal para testar diferentes payloads e analisar respostas.
- Exemplo: testar SQLi, XSS, fuzzing básico.

### 🔹 Intruder
- Automação de ataques.
- Permite injetar listas de payloads em diferentes posições da requisição.
- Útil para:
  - **Brute force** de logins.
  - **Fuzzing** de parâmetros.
  - **Descoberta de diretórios/arquivos**.

### 🔹 Scanner (somente na versão Pro)
- Faz análise **automática de vulnerabilidades**.
- Identifica problemas como:
  - **SQL Injection**
  - **XSS**
  - **CSRF**
  - **Misconfigurations**
- Não substitui teste manual, mas economiza tempo.

### 🔹 Decoder
- Codifica/decodifica dados em diferentes formatos:
  - Base64, URL encoding, HTML entities, Hex.
- Útil para analisar parâmetros escondidos ou ofuscados.

### 🔹 Comparer
- Compara duas respostas lado a lado.
- Usado para detectar mudanças sutis em respostas de testes.
- Exemplo: diferenciar resposta de login válido vs. inválido.

### 🔹 Sequencer
- Analisa **aleatoriedade de tokens** (sessão, autenticação, etc.).
- Mede entropia para verificar se o token pode ser **previsível**.

---

## 3. Fluxo de Uso Básico
1. Configurar o navegador para usar o **proxy do Burp (127.0.0.1:8080)**.  
2. Ativar o **Intercept** no Burp Suite.  
3. Navegar normalmente → requisições passam pelo Burp.  
4. Analisar, modificar e encaminhar requisições para o servidor.  
5. Usar módulos (Repeater, Intruder, etc.) para aprofundar testes.

---

## 4. Casos de Uso Comuns
- **Manipulação de cookies** → testar bypass de autenticação.  
- **Testes de SQL Injection** → enviar diferentes payloads via Repeater.  
- **Descoberta de parâmetros ocultos**.  
- **Força bruta em formulários de login** (Intruder).  
- **Validação de tokens JWT** (Decoder + Repeater).  
- **Exfiltração de dados** em cenários de XSS/CSRF.  

---

## 5. Integrações e Extensões
- **BApp Store** → marketplace de extensões oficiais e da comunidade.
- Exemplos úteis:
  - **JSON Web Tokens (JWT Editor)** – manipulação de JWT.
  - **Autorize** – teste de controle de acesso.
  - **Turbo Intruder** – automação de ataques mais rápidos.
  - **Logger++** – logging avançado de requisições.
  - **Flow** – visualização de fluxo de tráfego.

---

## 6. Versões do Burp Suite
- **Burp Suite Community (grátis)**:
  - Inclui Proxy, Repeater, Decoder, Comparer.
  - Não tem Scanner.
- **Burp Suite Professional (pago)**:
  - Inclui Scanner e funcionalidades avançadas.
- **Burp Suite Enterprise**:
  - Voltado para integração contínua (CI/CD) e empresas.

---

## 7. Boas Práticas de Uso
- Sempre usar **ambientes controlados ou autorizados**.
- Organizar os testes por etapas (mapear → analisar → explorar).
- Exportar e documentar **requisições vulneráveis**.
- Usar com **Firefox/Chromium + extensão FoxyProxy** para alternar rapidamente o proxy.
- Integrar com **wordlists** (SecLists) para ataques automatizados no Intruder.

---

## 8. Conclusão
O **Burp Suite** é uma das ferramentas mais importantes para **pentesters e bug bounty hunters**.  
Ele combina **interceptação, modificação e automação de ataques** em um só lugar, permitindo encontrar falhas em aplicações web de forma **eficiente e sistemática**.
