# Command Line – Cyber Security 101 (TryHackMe)

## 📌 Introdução
A **linha de comando (CLI – Command Line Interface)** permite interação direta com o sistema operacional.  
Na cibersegurança, o domínio da CLI é essencial, pois muitas ferramentas e técnicas são baseadas em **Linux** ou **Windows**.

---

# 🐧 Linux CLI

## 🌍 Navegação no Sistema de Arquivos
- `pwd` → mostra o diretório atual
- `ls` → lista arquivos e pastas
  - `ls -l` → detalhado
  - `ls -a` → inclui ocultos
- `cd pasta/` → entra em diretório
- `cd ..` → volta um nível
- `cd ~` → vai para `/home/usuario`

---

## 📂 Manipulação de Arquivos
- Criar:
  - `touch arquivo.txt`
  - `mkdir pasta`
- Visualizar:
  - `cat arquivo.txt`
  - `less arquivo.txt`
  - `head -n 10 arquivo.txt`
  - `tail -f log.txt`
- Remover:
  - `rm arquivo.txt`
  - `rm -r pasta/`
- Copiar/Mover:
  - `cp origem destino`
  - `mv origem destino`

---

## 🔀 Redirecionamento e Pipes
- `>` sobrescreve saída → `echo Teste > log.txt`
- `>>` adiciona saída → `echo Linha >> log.txt`
- `|` pipe → `cat arquivo.txt | grep senha`
- `2>` redireciona erros → `ls pasta_inexistente 2> erro.txt`

---

## 👥 Usuários e Permissões
- `whoami` → usuário atual
- `id` → mostra UID, GID e grupos
- `chmod 755 arquivo` → altera permissões
- `sudo comando` → executa como root
- `su usuario` → troca de usuário

---

## ⚙️ Processos
- `ps aux` → lista processos
- `top` ou `htop` → monitor em tempo real
- `kill PID` → encerra processo
- `killall nome` → encerra por nome

---

## 🌐 Rede
- `ip a` ou `ifconfig` → interfaces
- `ping google.com`
- `traceroute google.com`
- `curl http://site.com`
- `netstat -tulnp`

---

## 📜 Scripts
Exemplo `backup.sh`:
```bash
#!/bin/bash
tar -czf backup.tar.gz /home/usuario/documentos
echo "Backup concluído!"
```

# 🪟 Windows CLI – Cyber Security 101 (TryHackMe)

## 📌 Introdução
A **linha de comando no Windows** pode ser usada via **CMD** ou **PowerShell**.  
- **CMD** → mais simples, comandos herdados do DOS.  
- **PowerShell** → mais moderno, baseado em objetos, usado em automação e administração avançada.  

Dominar ambos é essencial para **cibersegurança, administração e automação**.

---

## 🌍 Navegação no Sistema de Arquivos
- `cd pasta` → entra em diretório
- `cd ..` → volta um nível
- `dir` → lista arquivos e pastas
- `echo %cd%` → exibe diretório atual (CMD)
- `Get-Location` → exibe diretório atual (PowerShell)

---

## 📂 Manipulação de Arquivos e Pastas
- Criar:
  - `echo. > arquivo.txt` → cria arquivo (CMD)
  - `New-Item arquivo.txt` → cria arquivo (PowerShell)
  - `mkdir pasta` → cria pasta
- Visualizar:
  - `type arquivo.txt` → mostra conteúdo (CMD)
  - `Get-Content arquivo.txt` → mostra conteúdo (PowerShell)
- Remover:
  - `del arquivo.txt`
  - `rmdir /s /q pasta` → remove pasta e conteúdo
  - `Remove-Item arquivo.txt` (PowerShell)
- Copiar/Mover:
  - `copy origem destino`
  - `move origem destino`
  - `Copy-Item origem destino` (PowerShell)
- Renomear:
  - `rename antigo.txt novo.txt`
  - `Rename-Item antigo.txt novo.txt` (PowerShell)

---

## 👥 Usuários e Permissões
- `whoami` → mostra usuário atual
- `net user` → lista usuários locais
- `net user novo senha /add` → cria usuário
- `icacls arquivo.txt` → exibe permissões de arquivo
- `runas /user:Administrador cmd` → abre cmd como admin
- PowerShell:
  - `Get-LocalUser` → lista usuários
  - `New-LocalUser -Name "teste" -Password (ConvertTo-SecureString "senha" -AsPlainText -Force)` → cria usuário

---

## ⚙️ Processos e Tarefas
- `tasklist` → lista processos ativos
- `taskkill /PID 1234 /F` → encerra processo pelo PID
- `taskkill /IM notepad.exe /F` → encerra processo por nome
- PowerShell:
  - `Get-Process` → lista processos
  - `Stop-Process -Id 1234` → encerra processo

---

## 🌐 Rede
- `ipconfig` → mostra interfaces e IP
- `ping google.com`
- `tracert google.com` → rastreia rota até o destino
- `netstat -ano` → mostra conexões e processos vinculados
- PowerShell:
  - `Test-Connection google.com`
  - `Get-NetTCPConnection`

---

## 📜 Scripts

### Batch (.bat)
```bat
@echo off
echo Criando backup...
xcopy C:\Users\Raphael\Documents D:\Backup\ /E /I /Y
echo Backup concluído!
pause
