# Linux Fundamentals

## 🔹 1. O que é Linux?
- **Linux:** Sistema operacional baseado no kernel criado por Linus Torvalds (1991).
- É **open source** e usado em servidores, dispositivos móveis (Android), IoT e até sistemas embarcados.
- Baseado em filosofia **Unix-like**.
- Diferente do Windows (GUI por padrão), o Linux é fortemente baseado em **CLI (Command Line Interface)**.

---

## 🔹 2. Estrutura do Sistema de Arquivos
O Linux organiza tudo em uma árvore de diretórios, a partir do **/** (root).
Principais diretórios:

- `/` → raiz do sistema.
- `/bin` → binários essenciais (ex.: ls, cp, mv).
- `/sbin` → binários administrativos (ex.: ifconfig, shutdown).
- `/etc` → arquivos de configuração.
- `/home` → diretórios dos usuários.
- `/root` → diretório do superusuário.
- `/tmp` → arquivos temporários.
- `/var` → arquivos variáveis (logs, spool).
- `/usr` → programas e bibliotecas do usuário.
- `/dev` → dispositivos representados como arquivos.
- `/proc` → informações do kernel e processos.

---

## 🔹 3. Navegação básica
Comandos essenciais:

```bash
pwd       # mostra diretório atual
ls        # lista arquivos
ls -la    # lista arquivos com detalhes (inclui ocultos)
cd /path  # muda de diretório
```

Atalhos:
- `.` → diretório atual
- `..` → diretório pai
- `~` → home do usuário

---

## 🔹 4. Manipulação de arquivos e diretórios
```bash
touch arquivo.txt        # cria arquivo vazio
mkdir pasta              # cria diretório
cp arquivo.txt destino/  # copia arquivo
mv arquivo.txt destino/  # move arquivo
rm arquivo.txt           # remove arquivo
rm -r pasta/             # remove diretório e conteúdo
```

---

## 🔹 5. Visualizar e editar arquivos
```bash
cat arquivo.txt          # mostra conteúdo
less arquivo.txt         # visualiza conteúdo (página a página)
head arquivo.txt         # primeiras linhas
tail arquivo.txt         # últimas linhas
nano arquivo.txt         # editor de texto simples
vim arquivo.txt          # editor avançado
```

---

## 🔹 6. Permissões de arquivos
Cada arquivo tem dono, grupo e permissões:
```
-rwxr-xr--  1 user  group  1024 Aug 17  arquivo.sh
```

- **Tipos de permissão:**
  - `r` → leitura
  - `w` → escrita
  - `x` → execução

- **Mudando permissões:**
```bash
chmod 755 arquivo.sh   # rwx para dono, rx para grupo e outros
chmod u+x script.sh    # adiciona execução para o dono
```

- **Mudando dono/grupo:**
```bash
chown user:group arquivo.txt
```

---

## 🔹 7. Usuários e grupos
- Usuário root = administrador.
- Arquivo `/etc/passwd` → informações de usuários.
- Arquivo `/etc/shadow` → senhas (hashes).

Comandos:
```bash
whoami        # mostra usuário atual
id            # mostra UID e GID
adduser nome  # adiciona usuário
passwd nome   # muda senha
su - usuario  # troca de usuário
sudo comando  # executa comando como root
```

---

## 🔹 8. Processos e serviços
- Cada programa rodando é um **processo**.
- PID = Process ID.

Comandos:
```bash
ps aux              # lista processos
top                 # monitor em tempo real
htop                # versão melhorada (se instalada)
kill -9 PID         # encerra processo
systemctl status    # mostra status do sistema
systemctl start ssh # inicia serviço
systemctl stop ssh  # para serviço
```

---

## 🔹 9. Gerenciamento de pacotes
Depende da distribuição:
- **Debian/Ubuntu (APT):**
```bash
sudo apt update
sudo apt install nmap
sudo apt remove nmap
```

- **Arch Linux (Pacman):**
```bash
sudo pacman -Syu
sudo pacman -S nmap
sudo pacman -R nmap
```

- **Red Hat/CentOS (YUM/DNF):**
```bash
sudo yum install nmap
sudo dnf install nmap
```

---

## 🔹 10. Redirecionamento e Pipes
- `>` → redireciona saída para arquivo (sobrescreve).
- `>>` → redireciona saída para arquivo (acrescenta).
- `<` → lê de um arquivo.
- `|` → conecta saída de um comando na entrada de outro.

Exemplos:
```bash
ls > lista.txt
cat arquivo.txt | grep "erro"
```

---

## 🔹 11. Variáveis e ambiente
- Variáveis de ambiente → configuram comportamento do sistema.
```bash
echo $HOME
echo $PATH
export VAR=valor
```

---

## 🔹 12. Arquivos importantes
- `/etc/passwd` → informações de usuários.
- `/etc/shadow` → senhas (hashes).
- `/etc/hosts` → mapeamento manual de hosts.
- `/etc/resolv.conf` → configuração de DNS.
- `/var/log/` → logs do sistema.

---

## 🔹 13. Redes no Linux
```bash
ifconfig / ip a     # mostra interfaces
ping 8.8.8.8        # testa conectividade
netstat -tulnp      # mostra conexões e portas (se instalado)
ss -tulnp           # substituto moderno do netstat
```

---

## 🔹 14. Arquivos compactados
```bash
tar -cvf arquivo.tar pasta/       # cria tar
tar -xvf arquivo.tar              # extrai tar
gzip arquivo.txt                  # compacta gzip
gunzip arquivo.txt.gz             # descompacta gzip
```

---

## 🔹 15. Segurança básica
- Evitar usar root para tarefas comuns.
- Usar `sudo` em vez de `su`.
- Definir permissões corretas em arquivos.
- Monitorar `/var/log/auth.log` para login suspeito.
- Usar `chmod` e `chown` corretamente.

---

## 🔹 16. Ferramentas úteis no Pentest
- `nmap` → scanner de rede.
- `tcpdump` → captura pacotes.
- `wireshark` → análise gráfica de pacotes.
- `netcat` (nc) → conexões manuais, backdoors.
- `hydra` → força bruta de senhas.
- `john` → quebra de hashes.

---

## 🔹 17. Exemplos práticos
- Criando usuário e testando login:
```bash
sudo adduser teste
su - teste
```

- Criando script simples:
```bash
#!/bin/bash
echo "Hello, Linux!"
```
```bash
chmod +x script.sh
./script.sh
```

- Encerrando processo que travou:
```bash
ps aux | grep firefox
kill -9 PID
```

---

## 🔹 18. Linux em segurança ofensiva
- Usado em **servidores** → alvo comum em ataques.
- **Permissões mal configuradas** → privilege escalation.
- **Logs** revelam informações sensíveis.
- **Ferramentas de hacking** são otimizadas para Linux (Kali, Parrot, BlackArch).

# Linux Básico – Command Line (TryHackMe)

## O que aprendi
- Conceito de **CLI (Command Line Interface)** e diferença para GUI.
- Navegação no sistema de arquivos:
  - `pwd` → mostra diretório atual
  - `ls` → lista arquivos
  - `cd` → navega entre pastas
- Manipulação de arquivos e diretórios:
  - `touch arquivo.txt` → cria arquivo
  - `mkdir pasta` → cria pasta
  - `rm arquivo.txt` → remove arquivo
  - `rm -r pasta/` → remove pasta recursivamente
- Leitura de arquivos:
  - `cat`, `less`, `head`, `tail`
- Redirecionamento e pipes:
  - `>` sobrescreve saída
  - `>>` adiciona à saída
  - `|` conecta comandos
- Permissões básicas:
  - `chmod` altera permissões
  - `ls -l` visualiza permissões
- Comandos úteis:
  - `echo`, `whoami`, `man`, `history`, `clear`

## Observações
- CLI dá muito mais controle que GUI.  
- Essencial para administração de sistemas e pentest.  
- Esse módulo serviu de base para aprofundar em Linux Fundamentals.

