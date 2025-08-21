# 🧰 John the Ripper – The Basics

John the Ripper (JtR) é uma ferramenta de **cracking de senhas** amplamente usada em testes de penetração, auditorias de segurança e pentesting. Ele ajuda a identificar **senhas fracas ou vulneráveis** em sistemas locais ou arquivos de hash, permitindo que administradores e profissionais de cibersegurança reforcem a segurança.

Conceitos fundamentais:
- Funciona em sistemas **Linux, Unix, macOS e Windows**.  
- Suporta vários tipos de hashes, incluindo **DES, MD5, SHA, bcrypt, Kerberos, Windows LM/NTLM**.  
- Utiliza **ataques por força bruta, dicionário e combinados** para tentar descobrir senhas.  
- É uma ferramenta de auditoria: deve ser usada apenas em ambientes **autorizados**.

Modos de ataque:
- **Dicionário:** usa listas de palavras (wordlists) para tentar combinações comuns de senhas.  
- **Força bruta:** tenta todas as combinações possíveis dentro de um conjunto definido de caracteres.  
- **Incremental:** otimizado para tentar combinações prováveis primeiro.  
- **Combinatório e híbrido:** combina ataques de dicionário com variações (ex.: substituir letras por números).

Exemplos de uso:
```bash
# Testar hashes em um arquivo com wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Mostrar senhas já quebradas
john --show hashes.txt

# Rodar ataque de força bruta
john --incremental hashes.txt
```
Opções importantes:
- **wordlist=<arquivo>** → define a lista de palavras para ataque de dicionário.
- **rules** → aplica regras de mutação à wordlist (ex.: adicionar números, trocar letras).
- **incremental** → modo de ataque por força bruta otimizado.
- **format=<tipo>** → especifica o tipo de hash (ex.: md5, sha256, des).
- **show** → mostra senhas quebradas de um arquivo de hashes.

# Conclusão
John the Ripper é essencial para avaliar a robustez de senhas e reforçar políticas de autenticação. Com preparação correta dos hashes, escolha apropriada de formato, wordlists + regras e monitoramento de sessão, você obtém resultados eficientes e reprodutíveis para auditorias profissionais.
