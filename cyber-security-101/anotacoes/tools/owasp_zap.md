# OWASP ZAP – Tools

## 1. O que é o OWASP ZAP?
- O **Zed Attack Proxy (ZAP)** é uma ferramenta open-source da **OWASP**.  
- Criada para **testes de segurança em aplicações web**.  
- Similar ao **Burp Suite**, mas **gratuita e open-source**.  
- Indicada tanto para **iniciantes** quanto para **profissionais**.  

---

## 2. Estrutura e Componentes Principais

### 🔹 Proxy
- Atua como intermediário entre **navegador ↔ servidor**.  
- Permite **interceptar, inspecionar e modificar** requisições e respostas.  

### 🔹 Spider
- Faz crawling do site para mapear todas as páginas, parâmetros e links.  
- Ajuda na **descoberta de superfícies de ataque**.  

### 🔹 Active Scan
- Realiza **varredura ativa** para identificar vulnerabilidades.  
- Testa falhas como:
  - SQL Injection  
  - Cross-Site Scripting (XSS)  
  - CSRF  
  - Directory Traversal  

### 🔹 Passive Scan
- Analisa o tráfego **sem alterar requisições**.  
- Identifica problemas como:
  - Cabeçalhos de segurança ausentes  
  - Informações sensíveis expostas  
  - Cookies inseguros  

### 🔹 Fuzzer
- Permite inserir diferentes payloads em parâmetros.  
- Útil para **brute force, fuzzing e descoberta de parâmetros ocultos**.  

### 🔹 Session Management
- Gerencia autenticação, cookies e tokens de sessão.  
- Permite simular usuários autenticados.  

### 🔹 Report Generator
- Cria relatórios detalhados com as vulnerabilidades encontradas.  
- Útil para documentar testes.  

---

## 3. Fluxo de Uso Básico
1. Configurar o navegador para usar o **proxy do ZAP (127.0.0.1:8080)**.  
2. Ativar **Intercept** para capturar tráfego.  
3. Usar o **Spider** para mapear a aplicação.  
4. Realizar **Passive Scan** para identificar problemas básicos.  
5. Executar **Active Scan** para encontrar vulnerabilidades.  
6. Validar falhas manualmente usando o **Fuzzer** ou o **Request Editor**.  

---

## 4. Casos de Uso Comuns
- Mapear endpoints ocultos da aplicação.  
- Testar **injeção de parâmetros** (SQLi, XSS).  
- Avaliar **segurança de autenticação e sessões**.  
- Fazer **fuzzing de inputs**.  
- Detectar configurações incorretas de cabeçalhos de segurança.  

---

## 5. Extensões e Add-ons
- O ZAP tem um **marketplace interno** para instalar add-ons.  
- Exemplos úteis:
  - **JWT Support** – manipulação de tokens JWT.  
  - **GraphQL Add-on** – testes em APIs GraphQL.  
  - **WebSockets** – análise de tráfego WebSocket.  
  - **HUD (Heads Up Display)** – integração no navegador para feedback em tempo real.  

---

## 6. Diferenças entre Burp Suite e ZAP
- **Burp Suite**:
  - Mais usado no mercado.  
  - Versão Pro tem **Scanner avançado**.  
  - Pago (versão Community é limitada).  
- **OWASP ZAP**:
  - 100% gratuito e open-source.  
  - Mais acessível para iniciantes.  
  - Possui boa automação, mas menos refinado que Burp.  

---

## 7. Boas Práticas
- Usar ZAP em conjunto com wordlists como **SecLists**.  
- Configurar **contexts** para diferentes usuários/sessões.  
- Integrar com **CI/CD pipelines** (DevSecOps).  
- Sempre validar manualmente resultados do **Active Scan**.  

---

## 8. Conclusão
O **OWASP ZAP** é uma excelente alternativa gratuita ao **Burp Suite**, com recursos poderosos de **interceptação, fuzzing e escaneamento automático**.  
É ideal para **quem está começando** e também útil em pipelines de segurança corporativos.
