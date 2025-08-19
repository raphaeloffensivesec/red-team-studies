# Desafio – Inspecionando Headers

### Usando curl:
```bash
curl -I http://example.com
```

### Saída esperada:
```
HTTP/1.1 200 OK
Date: Sun, 17 Aug 2025 22:10:00 GMT
Server: nginx/1.18.0
Content-Type: text/html
```

### Observações:
- `Server` mostra o backend (pode ser ocultado em produção).
- `Content-Type` define o formato da resposta.
- Headers são chave para análise de segurança.

