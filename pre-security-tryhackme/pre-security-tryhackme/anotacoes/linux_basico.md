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

