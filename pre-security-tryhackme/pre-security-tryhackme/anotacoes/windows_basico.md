# Windows Fundamentals – Anotações

## 1. Estrutura de Diretórios
- `C:\` – raiz do sistema.
- `C:\Windows` – arquivos principais do sistema.
- `C:\Users` – perfis dos usuários.
- `C:\Program Files` – programas instalados.

### Diretórios importantes
- `%SystemRoot%` → normalmente `C:\Windows`.
- `%USERPROFILE%` → pasta pessoal do usuário.
- `%TEMP%` → arquivos temporários.

---

## 2. Prompt de Comando (CMD)
- `dir` → lista arquivos.
- `cd` → muda diretório.
- `cls` → limpa tela.
- `echo` → exibe texto.
- `copy` / `move` / `del` → copiar, mover e apagar arquivos.

### Operadores
- `>` → redireciona saída para arquivo.
- `>>` → adiciona ao final do arquivo.
- `|` → pipe (ex.: `dir | find "txt"`).

---

## 3. PowerShell
- `Get-Process` → lista processos.
- `Get-Service` → lista serviços.
- `Get-Help` → ajuda.
- `Get-Command` → lista todos os comandos.
- `Select-String` → equivalente ao `grep` no Linux.

Exemplo:
```powershell
Get-ChildItem C:\Users -Recurse -Include *.txt

