# Desafio – Testando Requisições HTTP

### Usando curl (Linux/macOS/WSL):
```bash
# GET request
curl -v http://example.com

# POST request
curl -X POST -d "usuario=admin&senha=123" http://example.com/login
```

### Usando PowerShell (Windows):
```powershell
Invoke-WebRequest -Uri "http://example.com" -Method GET
Invoke-WebRequest -Uri "http://example.com/login" -Method POST -Body "usuario=admin&senha=123"
```

