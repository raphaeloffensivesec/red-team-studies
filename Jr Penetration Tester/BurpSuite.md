# Burp Suite – TryHackMe

O **Burp Suite** é a ferramenta padrão da indústria para **Web Application Pentesting**, atuando como intermediário entre cliente e servidor.  
Através dele é possível inspecionar, modificar e automatizar requisições HTTP/S, identificar falhas e explorar vulnerabilidades em aplicações web.  

Este módulo do TryHackMe apresentou de forma prática os principais recursos da ferramenta, mostrando como cada um pode ser utilizado em cenários reais de pentest.

---

## 🔹 1. Burp Suite: The Basics
- **Configuração inicial**
  - Instalação do certificado do Burp para interceptação HTTPS.
  - Ajuste do proxy no navegador (usando FoxyProxy no Firefox).
- **Interceptação de tráfego**
  - Captura de requisições HTTP e HTTPS entre o cliente e o servidor.
  - Manipulação de cabeçalhos, parâmetros GET e POST antes do envio.
- **Proxy History**
  - Registro detalhado de todas as requisições capturadas.
  - Possibilidade de enviar requisições específicas para ferramentas internas (Repeater, Intruder, etc.).

📌 **Exemplo prático:** interceptar o envio de um formulário de login, modificar o parâmetro `username` e reenviar para analisar como o servidor responde.

---

## 🔹 2. Burp Suite: Repeater
- **Função principal:** testar manualmente vulnerabilidades repetindo e alterando requisições.  
- **Aplicações comuns:**
  - Testar **SQL Injection** em campos de input (`' OR '1'='1--`).
  - Explorar **XSS** injetando payloads em parâmetros.
  - Alterar tokens de sessão ou cookies para verificar falhas de autenticação.
- **Benefícios:**
  - Controle total sobre o conteúdo da requisição.
  - Feedback imediato da resposta do servidor.

📌 **Exemplo prático:** enviar repetidamente a requisição de login com senhas diferentes para validar respostas diferenciadas do sistema.

---

## 🔹 3. Burp Suite: Intruder
- **Objetivo:** automatizar ataques enviando múltiplas requisições de forma sistemática.  
- **Tipos de ataque disponíveis:**
  - **Sniper:** testa payloads individualmente em um único ponto.
  - **Battering Ram:** usa o mesmo payload em múltiplos pontos simultaneamente.
  - **Pitchfork:** usa diferentes listas de payloads em paralelo.
  - **Cluster Bomb:** gera todas as combinações possíveis de payloads.
- **Aplicações práticas:**
  - **Força bruta em logins** (usuário/senha).
  - **Enumeração de parâmetros ocultos**.
  - **Fuzzing** de inputs para descobrir falhas de validação.
  - **Descoberta de diretórios/arquivos** no servidor (com wordlists).

📌 **Exemplo prático:** realizar brute-force contra um campo de login com uma lista de 1000 senhas comuns.

---

## 🔹 4. Burp Suite: Other Modules
Além das funções principais, o Burp Suite inclui módulos auxiliares fundamentais em pentests:

- **Decoder**
  - Codificação/decodificação de valores em Base64, URL, HTML, Hex.
  - Útil para analisar cookies ou parâmetros ofuscados.
- **Comparer**
  - Compara duas respostas diferentes, destacando variações sutis.
  - Ajuda a identificar diferenças entre login válido e inválido, por exemplo.
- **Sequencer**
  - Avalia a aleatoriedade de tokens de sessão e cookies.
  - Detecta vulnerabilidades em sistemas com geração previsível de tokens.
- **Logger/Proxy History**
  - Permite revisar todas as interações feitas entre cliente-servidor.
  - Facilita a análise forense durante um pentest.

📌 **Exemplo prático:** usar o Sequencer para avaliar a previsibilidade de tokens JWT emitidos por uma aplicação.

---

## 🔹 5. Burp Suite: Extensions
O Burp pode ser expandido através da **BApp Store** ou com scripts customizados em **Python/Java**.

- **Plugins populares:**
  - **Autorize:** verifica falhas de controle de acesso entre usuários (Horizontal/Vertical Privilege Escalation).
  - **Turbo Intruder:** versão otimizada do Intruder, ideal para fuzzing em larga escala.
  - **JSON Web Token Attacker (JWT):** auxilia na exploração de tokens inseguros.
  - **ActiveScan++:** melhora o scanner ativo de vulnerabilidades.
- **Benefício:** possibilita adaptar o Burp às necessidades do pentester, ampliando suas capacidades.

📌 **Exemplo prático:** usar o Autorize para verificar se um usuário comum consegue acessar endpoints restritos de administrador.

---

# 🛠️ Casos Reais de Uso
O conhecimento adquirido neste módulo pode ser aplicado em diversos cenários, tais como:
- **Testes de autenticação:** identificar senhas fracas e vulnerabilidades de login.
- **Exploração de parâmetros:** manipulação de inputs para SQLi, XSS e LFI.
- **Análise de tokens:** verificar segurança de sessões e JWTs.
- **Validação de acessos:** detectar falhas em controles de autorização.
- **Automatização de ataques:** executar milhares de tentativas em pouco tempo.

---

# 📌 Conclusão
Com este módulo do TryHackMe, adquiri proficiência nos principais recursos do **Burp Suite**, entendendo como:
- Interceptar e manipular tráfego web.  
- Testar e explorar manualmente vulnerabilidades.  
- Automatizar ataques em massa.  
- Utilizar módulos auxiliares para análises avançadas.  
- Ampliar a funcionalidade com extensões da comunidade.  

O **Burp Suite** é uma das ferramentas mais importantes em **pentest de aplicações web** e será utilizada de forma recorrente ao longo da minha jornada em **Red Team**.  

---
