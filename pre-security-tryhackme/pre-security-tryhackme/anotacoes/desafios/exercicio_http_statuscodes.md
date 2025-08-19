# Desafio – Testando Status Codes

1. Acesse:
   - `http://httpstat.us/200` → 200 OK
   - `http://httpstat.us/404` → 404 Not Found
   - `http://httpstat.us/500` → 500 Internal Server Error

2. Teste com curl:
```bash
curl -i http://httpstat.us/404
```

3. Observação:
- Útil para aprender como cada tipo de código é usado.
- Em testes de segurança, códigos **403** e **401** indicam restrição de acesso.
