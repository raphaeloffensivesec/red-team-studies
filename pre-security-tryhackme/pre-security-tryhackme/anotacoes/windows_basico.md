# 🪟 Windows Fundamentals – Anotações

Este documento reúne os principais conceitos e comandos vistos no módulo **Windows Fundamentals** do TryHackMe.  
Serve como guia rápido de estudo e referência.

---

## 📂 Estrutura de Diretórios

- `C:\` → raiz do sistema.
- `C:\Windows` → arquivos principais do sistema operacional.
- `C:\Users` → diretórios de cada usuário.
- `C:\Program Files` → programas instalados (64 bits).
- `C:\Program Files (x86)` → programas 32 bits.
- `C:\Temp` ou `%TEMP%` → arquivos temporários.

### Variáveis de ambiente
- `%SystemRoot%` → normalmente `C:\Windows`.
- `%USERPROFILE%` → pasta do usuário atual.
- `%APPDATA%` → dados de aplicativos.
- `%PATH%` → diretórios de execução de binários.

---

## 🖥️ Prompt de Comando (CMD)

### Comandos básicos
- `dir` → lista arquivos e pastas.
- `cd` → navegar entre diretórios.
- `cls` → limpa a tela.
- `echo` → exibe mensagens.
- `copy` / `move` / `del` → copiar, mover e excluir arquivos.
- `mkdir` / `rmdir` → criar e remover diretórios.

### Operadores úteis
- `>` → redireciona saída para um arquivo.  
  Ex: `dir > lista.txt`
- `>>` → adiciona saída ao final de um arquivo.  
  Ex: `echo teste >> notas.txt`
- `|` → pipe (encadear comandos).  
  Ex: `dir | find "txt"`

---

## ⚡ PowerShell

Mais poderoso que o CMD, suporta objetos e scripts.

### Principais comandos
- `Get-Command` → lista todos os comandos disponíveis.
- `Get-Help <comando>` → exibe ajuda de um comando.
- `Get-ChildItem` (alias: `ls`) → lista diretórios/arquivos.
- `Set-Location` (alias: `cd`) → muda de diretório.
- `Select-String` → busca em arquivos (equivalente ao `grep`).
- `Get-Process` → lista processos em execução.
- `Stop-Process -Id <pid>` → encerra processo.
- `Get-Service` → lista serviços.
- `Start-Service <nome>` / `Stop-Service <nome>` → inicia ou para serviço.

### Exemplo prático
```powershell
# Listar todos arquivos .txt dentro da pasta Users
Get-ChildItem C:\Users -Recurse -Include *.txt
