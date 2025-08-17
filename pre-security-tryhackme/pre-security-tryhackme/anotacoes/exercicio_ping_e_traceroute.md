# Desafio – Ping no Linux

```bash
ping -c 4 1.1.1.1
ping -c 4 tryhackme.com
```

### Observações
- Ping no IP funciona direto.
- Ping no domínio precisa resolver o DNS antes.

---
# Desafio – Ping no Windows

```powershell
ping 1.1.1.1
ping tryhackme.com
```

### Observações
- Funciona de forma parecida com o Linux, mas o parâmetro é diferente (`-n` em vez de `-c` para número de pacotes).
# Desafio – Traceroute no Linux

```bash
traceroute tryhackme.com
```

### Observações
- Mostra cada roteador até o destino.
- Útil para diagnosticar onde a conexão está lenta.

---
# Desafio – Traceroute no Windows

```powershell
tracert tryhackme.com
```

### Observações
- Mesmo conceito do Linux, mas o comando é `tracert`.
- Cada linha mostra um "salto" (roteador) no caminho.
