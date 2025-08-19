# 🪟 Windows Fundamentals – Anotações Completas

Este documento reúne **todos os conceitos, comandos, exemplos práticos e boas práticas de segurança** do módulo Windows Fundamentals do TryHackMe.  
Serve como guia de estudo, referência rápida e checklist para prática.

---

## 📂 Estrutura de Diretórios

O Windows organiza seus arquivos em uma hierarquia que facilita administração e segurança.

- `C:\` → raiz do sistema.
- `C:\Windows` → arquivos essenciais do sistema operacional.
- `C:\Users` → diretórios de usuários.
- `C:\Program Files` → programas instalados 64 bits.
- `C:\Program Files (x86)` → programas 32 bits.
- `%TEMP%` → arquivos temporários do usuário.
- `%APPDATA%` → dados de aplicativos.
- `%SystemRoot%` → normalmente `C:\Windows`.
- `%USERPROFILE%` → pasta pessoal do usuário.
- `%PATH%` → diretórios de execução de binários.

**Dicas importantes:**
- Evite alterar arquivos em `C:\Windows` sem necessidade.
- Sempre use permissões administrativas para alterações críticas.

---

## 🖥️ Prompt de Comando (CMD)

O CMD é útil para tarefas rápidas e automação básica.

### Comandos essenciais
- `dir` → lista arquivos e pastas (com `/a` mostra ocultos).
- `cd` → navega entre diretórios (`cd..` sobe um nível).
- `cls` → limpa a tela.
- `echo` → exibe mensagens.
- `copy` / `move` / `del` → copiar, mover ou excluir arquivos.
- `mkdir` / `rmdir` → criar ou remover diretórios.

### Operadores
- `>` → redireciona saída para um arquivo.  
  Ex: `dir > lista.txt`
- `>>` → adiciona ao final de um arquivo.  
  Ex: `echo teste >> notas.txt`
- `|` → pipe, encadeia comandos.  
  Ex: `dir | find "txt"`

### Dicas
- Sempre execute CMD como administrador para tarefas de rede ou sistema.
- Use `/s` e `/q` com `rmdir` para remover pastas recursivamente sem confirmação.

---

## ⚡ PowerShell

PowerShell é mais moderno, suporta objetos, automação e scripts.

### Comandos básicos
- `Get-Command` → lista comandos disponíveis.
- `Get-Help <comando>` → exibe ajuda detalhada.
- `Get-ChildItem` (`ls`) → lista arquivos e pastas.
- `Set-Location` (`cd`) → muda de diretório.
- `Select-String` → busca texto dentro de arquivos.
- `Get-Process` → lista processos ativos.
- `Stop-Process -Id <pid>` → encerra processos.
- `Get-Service` → lista serviços.
- `Start-Service <nome>` / `Stop-Service <nome>` → gerencia serviços.

### Exemplos práticos
```powershell
# Listar todos arquivos .txt no diretório do usuário
Get-ChildItem $env:USERPROFILE -Recurse -Include *.txt

# Ver processos ordenados por uso de CPU
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10

# Verificar portas abertas
Get-NetTCPConnection | Where-Object { $_.State -eq "Listen" }
