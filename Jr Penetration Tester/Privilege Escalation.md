# Privilege Escalation – Jr Penetration Tester (TryHackMe)

Este documento reúne minhas anotações completas da seção **Privilege Escalation** do caminho **Jr Penetration Tester**. O foco é transformar um **acesso inicial limitado** em **controle total** da máquina (root em Linux, SYSTEM/Administrator em Windows) por meio de **enumeração cuidadosa** e **abuso de más configurações** conhecidas.

---

## Visão Geral
- Objetivo: sair de usuário restrito para root/SYSTEM.
- Estratégia: 1) estabilizar a shell, 2) enumerar ao máximo, 3) priorizar vetores prováveis, 4) explorar com segurança, 5) persistir e coletar provas, 6) limpar rastros.
- Regra de ouro: quase toda escalada de privilégio vem de **informação** (enumeração) + **má configuração** (ou versão vulnerável).

---

## 1) What the Shell? (estabilização e ergonomia)

### Tipos de acesso comuns
- Reverse shell: a vítima conecta de volta para meu host.
- Bind shell: a vítima abre uma porta; eu me conecto.
- Web shell: execução de comandos via HTTP (php, asp, aspx, jsp, etc.).
- TTY interativo vs pseudo-TTY: shells “cruas” costumam não ter histórico, Ctrl+C, setas.

### Estabilização e melhorias rápidas (Linux)
- Promover TTY: `python3 -c 'import pty; pty.spawn("/bin/bash")'`, depois `export TERM=xterm`, suspender com `Ctrl+Z`, então `stty raw -echo; fg`.
- Ajustar PATH e locale se necessário: `echo $PATH`, `export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin`.
- Checar rede para callbacks: `ip a`, `ss -tulpn`, `ip route`.

### Boas práticas
- Registrar tudo: diretório de trabalho para artefatos e logs.
- Não “quebrar” o alvo: validar comandos com `which` e `type` antes de executar.
- Usar `script` ou `scriptreplay` se disponível para gravar a sessão.

---

## 2) Linux Privilege Escalation

### 2.1 Enumeração essencial (manual)
- Identidade e contexto: `id`, `whoami`, `groups`, `hostname`.
- Sistema: `uname -a`, `cat /etc/os-release`, `lsb_release -a`.
- Sudoers: `sudo -l` (ver se há NOPASSWD, comandos permitidos).
- Arquivos e permissões: `ls -la ~`, `ls -la /tmp /var/tmp`, `umask`.
- Serviços e processos: `ps aux`, `systemctl list-units --type=service`, `crontab -l`, `ls -la /etc/cron*`, `journalctl -xe` (se permitido).
- Rede: `ip a`, `ip r`, `ss -tunlp`, arquivos de config em `/etc/hosts` e `/etc/resolv.conf`.
- Montagens e NFS: `mount`, `cat /etc/fstab`, `showmount -e <host>` quando aplicável.
- Bins SUID/CAP: `find / -perm -4000 -type f 2>/dev/null`, `getcap -r / 2>/dev/null`.
- Credenciais: `grep -ri "password\|passwd\|PWD\|SECRET" /etc /opt /var /home 2>/dev/null`, `cat ~/.ssh/*`, `history`.

### 2.2 Enumeração automatizada (quando possível)
- LinPEAS (preferido), LinEnum, linux-smart-enumeration, pspy (ver cron/serviços), linux-exploit-suggester (kernel e CVEs).

### 2.3 Vetores clássicos (com checagens e exemplos)

1. Sudo mal configurado  
   - Sinais: `sudo -l` mostra comandos com `NOPASSWD`.  
   - Ação: consultar GTFOBins para o binário listado (ex.: `sudo vim -c ':!/bin/sh'`, `sudo find . -exec /bin/sh \; -quit`, `sudo less` com `!sh`).  
   - Mitigação (defensiva): remover NOPASSWD, usar `sudoers` restritivo e `requiretty` quando aplicável.

2. Binaries SUID/SGID  
   - Sinais: bins fora do padrão (`/usr/local/bin`), linguagens (`python`, `perl`, `node`) ou utilitários (tar, cp, bash) com bit SUID.  
   - Ação: usar GTFOBins para “SUID Escalation”. Exemplos: `./bash -p`, `python -c 'import os; os.setuid(0); os.system("/bin/sh")'` quando SUID.  
   - Nota: em distros modernas, `bash -p` respeita SUID; caso contrário, procurar alternativas.

3. Linux Capabilities  
   - Sinais: `getcap -r /` revela algo como `/usr/bin/python3 cap_setuid+ep`.  
   - Ação: abusar da capability (ex.: em python, fazer `os.setuid(0)`).  
   - Defesa: revisar capabilities, evitar conceder `cap_setuid` e similares.

4. PATH hijacking / scripts root  
   - Sinais: scripts root com uso de binários sem caminho absoluto (ex.: `tar` em vez de `/bin/tar`), `env` perigoso.  
   - Ação: colocar bin falso em diretório anterior no `PATH` e forçar execução via cron/serviço.  
   - Dica: procurar em `/etc/cron*` e scripts em `/opt` e `/usr/local/bin`.

5. Cron jobs e timers  
   - Sinais: `crontab -l`, `ls -la /etc/cron.*`, `systemctl list-timers`.  
   - Ação: se script é editável por usuário e roda como root, injetar payload seguro (ex.: criar arquivo controlado).  
   - Atenção: não derrubar serviços de produção.

6. NFS e no_root_squash  
   - Sinais: export com `no_root_squash`.  
   - Ação: montar export, criar arquivo SUID root e sincronizar de volta para host.  
   - Defesa: nunca usar `no_root_squash` em produção.

7. Docker/LXD e grupos privilegiados  
   - Sinais: `groups` contém `docker`, `lxd`.  
   - Ação: em docker, rodar container montando `/` e chroot; em LXD, iniciar contêiner privilegiado e montar host.  
   - Defesa: remover usuários desses grupos.

8. Arquivos sensíveis graváveis  
   - Sinais: `/etc/passwd` gravável ou scripts de serviço root graváveis.  
   - Ação: se `/etc/passwd` for gravável, criar hash de senha com `openssl passwd -1` e adicionar usuário root-like; em serviços, substituir binário ou config para rodar comando.

9. Credenciais em claro e reaproveitamento  
   - Fontes: `.bash_history`, `.env`, configs de apps web, backups `.bak`/`.old`, dumps DB.  
   - Reaproveitar em `sudo`, `su`, `ssh`, painéis web internos.

10. Kernel exploits (último recurso)  
   - Sinais: kernel muito antigo reportado pelo enumerador.  
   - Ação: pesquisar CVEs específicos (ex.: Dirty COW, OverlayFS, polkit/PKEXEC), baixar e compilar com cuidado.  
   - Risco: instabilidade do sistema; preferir vetores lógicos primeiro.

### 2.4 Pós-escalada (Linux)
- Verificar identidade: `id`, `whoami`.  
- Coletar provas: caminhos de exploração, configs, capturas de tela/logs.  
- Criar persistência ética (se escopo permitir): adicionar chave em `~/.ssh/authorized_keys`, tarefa agendada, serviço controlado.  
- Limpeza: remover arquivos temporários, restaurar permissões.

---

## 3) Windows Privilege Escalation

### 3.1 Enumeração essencial (manual)
- Identidade e grupos: `whoami`, `whoami /all`, `whoami /priv`, `whoami /groups`.
- Sistema: `systeminfo` (conferir build, hotfixes), `wmic qfe get hotfixid`.
- Processos/serviços: `tasklist /v`, `sc query`, `sc qc <serviço>`.
- Rede: `ipconfig /all`, `route print`, `netstat -ano`.
- Usuários/grupos: `net user`, `net localgroup administrators`.
- ACLs e integridade: `icacls <caminho>`, `wmic integrity`.
- Locais de credenciais: `%APPDATA%`, `%PROGRAMDATA%`, `C:\Users\<user>\AppData\Roaming`, `C:\Windows\Panther\Unattend.xml`, `sysprep.inf`, `web.config`, arquivos `.kdbx`, `RDCMan.settings`.

### 3.2 Enumeração automatizada
- winPEAS (completo), Seatbelt (coleta direcionada), SharpUp/PowerUp (procura vetores de privilégio), PowerView (domínio), AccessChk (permissões em arquivos/serviços), PrivescCheck.

### 3.3 Vetores clássicos (com checagens e exemplos)

1. Serviços vulneráveis  
   - Unquoted Service Path: caminho com espaços sem aspas permite substituir binários no caminho. Checar com `sc qc <serviço>`.  
   - Permissões fracas no serviço/binário: detectar com AccessChk (`accesschk.exe -uwcqv "Users" "C:\Path\bin.exe"`).  
   - Ação: substituir binário ou alterar `binPath` com `sc config <serviço> binPath= "cmd /c <payload>"` se permitido; iniciar com `sc start <serviço>`.

2. AlwaysInstallElevated (MSI como Admin)  
   - Checagem: `reg query HKCU\Software\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated` e mesmo em HKLM; se ambos 1, possível elevar executando `msiexec /quiet /qn /i evil.msi`.

3. Programas em execução como SYSTEM com arquivos graváveis  
   - Ex.: serviços que carregam configs `.xml`/`.ini` graváveis.  
   - Ação: troca de caminho de log, drop de DLL ou injeção de config.

4. DLL Hijacking / Search Order  
   - Aplicativos procuram DLLs sem caminho absoluto.  
   - Ação: colocar DLL maliciosa no diretório preferencial.  
   - Dica: monitorar com ProcMon para ver “NAME NOT FOUND”.

5. Task agendada/atualizações customizadas  
   - Checagem: `schtasks /query /fo LIST /v`.  
   - Ação: se script/EXE chamado pela tarefa for gravável pelo usuário, trocá-lo.

6. Token Impersonation e Named Pipes  
   - Situação: serviço com SeImpersonatePrivilege disponível.  
   - Ação: usar PrintSpoofer/Rotten/JuicyPotato (dependendo da versão) para capturar e impersonar token SYSTEM.

7. UAC Bypass (quando já é Admin local)  
   - Apenas quando conta já é Administrators e há UAC: abusa de autoelevate ou COM handlers.  
   - Não confundir com privesc a partir de usuário padrão.

8. LAPS/GPP e segredos em GPO/AD  
   - GPP antigo expõe `cpassword` (AES fixo) em `Groups.xml`.  
   - LAPS mal configurado pode vazar senha no atributo do computador.

9. Credenciais em memória e SAM/SECURITY  
   - Se `SeDebugPrivilege`, usar Mimikatz (`privilege::debug`, `sekurlsa::logonpasswords`).  
   - Dump offline de `C:\Windows\System32\config\SAM` e `SYSTEM` para cracking.  
   - DPAPI: `mimikatz dpapi::cred /in:<arquivo>` quando chaves disponíveis.

10. Vulnerabilidades de kernel/driver (último recurso)  
   - Cross-check com `systeminfo` e listas de CVEs (ex.: MS16-032 em sistemas muito antigos).  
   - Alto risco operacional; preferir lógicas e ACLs primeiro.

### 3.4 Pós-escalada (Windows)
- Validar: `whoami`, `echo %USERNAME%`, `whoami /groups` confirma `NT AUTHORITY\SYSTEM`.  
- Coleta de evidências: versão, serviço vulnerável, permissões indevidas, prova de execução elevada.  
- Persistência ética (se escopo permitir): novo serviço, agendamento, chave de registro Run/RunOnce, RDP habilitado com conta dedicada.  
- Limpeza: remover binários, restaurar caminhos de serviço, apagar chaves temporárias.

---

## 4) Checklist rápido (operacional)

1. Estabilizar shell e verificar conectividade.  
2. Enumerar tudo (automático + manual).  
3. Procurar: `sudo -l`, SUID, capabilities, cron, NFS, grupos privilegiados, serviços, arquivos graváveis, credenciais.  
4. Priorizar vetores “seguros e lógicos” antes de kernel exploits.  
5. Executar exploração mínima e verificável; guardar hash/artefatos de PoC.  
6. Confirmar privilégio, coletar evidências e, se permitido, persistir.  
7. Remediar/limpar para não deixar o host pior do que foi encontrado.

---

## 5) Referências úteis (para consulta rápida)
- GTFOBins (Linux): técnicas para SUID/sudo.  
- LOLBAS (Windows): Living Off The Land Binaries.  
- LinPEAS/winPEAS, Seatbelt, PowerUp, AccessChk.  
- OWASP Testing Guide (seção de privesc contextual).  

---

## 6) Observações finais
- Em ambientes de treino (como TryHackMe), validar cada vetor de forma controlada e documentar exatamente o que permitiu a escalada.  
- Em ambientes reais, alinhar com escopo e regras; evitar técnicas de alto risco (exploits de kernel) quando há alternativas de configuração/ACL.  
- O sucesso na escalada quase sempre vem de **boa enumeração + atenção a detalhes**: um `sudo -l` esquecido, um serviço com ACL frouxa, um cron com script gravável, um `docker` no grupo do usuário ou um caminho sem aspas já são suficientes para chegar ao topo.

