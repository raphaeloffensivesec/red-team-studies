# 🔐 Cryptography – Cyber Security 101

## 📌 Introdução
A criptografia é a ciência de proteger informações, garantindo **confidencialidade, integridade, autenticidade e não-repúdio**.  
É essencial em cibersegurança para comunicação segura, armazenamento de dados, autenticação de usuários e proteção de sistemas críticos.  
Nesta seção, abordamos conceitos teóricos e exemplos práticos de **cifras, hashing, protocolos e ferramentas**.

---

## 🔹 Conceitos Fundamentais
- **Confidencialidade:** apenas usuários autorizados podem acessar os dados.  
- **Integridade:** dados não podem ser alterados sem detecção.  
- **Autenticidade:** valida identidade do remetente e receptor.  
- **Não-repúdio:** garante que uma ação ou envio não possa ser negado pelo emissor.  
- **Criptografia vs Codificação:** criptografia protege a informação; codificação transforma dados para transmissão, mas não é segura.

---

## 🔹 Tipos de Criptografia

### Simétrica
- Mesma chave usada para criptografar e descriptografar.
- **Vantagens:** rápida e eficiente para grandes volumes de dados.  
- **Desvantagens:** problema de distribuição segura da chave.  
- **Algoritmos comuns:** AES (Advanced Encryption Standard), DES, 3DES, Blowfish.  
- **Uso:** VPNs, armazenamento seguro, criptografia de disco (BitLocker, LUKS).

**Exemplo prático com OpenSSL:**
```bash
# Criptografar arquivo com AES-256
openssl enc -aes-256-cbc -salt -in arquivo.txt -out arquivo.enc

# Descriptografar
openssl enc -aes-256-cbc -d -in arquivo.enc -out arquivo_decrypted.txt
```

# Assimétrica 

A criptografia assimétrica utiliza **duas chaves distintas**: uma **pública** para criptografar dados e uma **privada** para descriptografar. É fundamental para **comunicação segura, assinaturas digitais e autenticação**.

Conceitos principais:
- **Chave pública:** distribuída abertamente, usada para criptografar mensagens.  
- **Chave privada:** mantida em segredo pelo proprietário, usada para descriptografar mensagens.  
- **Vantagens:** permite comunicação segura sem compartilhar a chave privada; suporta assinaturas digitais.  
- **Desvantagens:** mais lenta que criptografia simétrica; requer gerenciamento seguro de chaves.

Algoritmos comuns:
- **RSA:** amplamente usado em SSL/TLS, emails seguros e certificados digitais.  
- **ECC (Elliptic Curve Cryptography):** eficiente e segura com chaves menores; usada em mobile e IoT.  
- **ElGamal:** usado em PGP e algumas implementações de chave pública.

Uso típico:
- **SSL/TLS:** garante comunicação segura na web (HTTPS).  
- **Emails seguros:** PGP/GPG.  
- **Assinaturas digitais:** valida documentos e mensagens.  
- **Autenticação:** verificação de identidade sem compartilhar senha.

Exemplos práticos com OpenSSL:
```bash
# Gerar chave privada RSA de 2048 bits
openssl genrsa -out private.key 2048

# Gerar chave pública a partir da privada
openssl rsa -in private.key -pubout -out public.key

# Criptografar arquivo com a chave pública
openssl rsautl -encrypt -inkey public.key -pubin -in mensagem.txt -out mensagem.enc

# Descriptografar arquivo com a chave privada
openssl rsautl -decrypt -inkey private.key -in mensagem.enc -out mensagem_decrypted.txt

# Criar assinatura digital
openssl dgst -sha256 -sign private.key -out assinatura.sig mensagem.txt

# Verificar assinatura digital
openssl dgst -sha256 -verify public.key -signature assinatura.sig mensagem.txt
```
# Hashing 

Hashing é um processo que gera um **resumo fixo de dados de tamanho variável** de forma unidirecional, ou seja, não é possível reverter o hash para obter os dados originais. É essencial para **armazenamento seguro de senhas, verificação de integridade e assinaturas digitais**.

Conceitos principais:
- Função de hash gera um valor único (digest) para cada entrada.  
- Pequenas mudanças nos dados produzem hash completamente diferente.  
- Irreversível: não é possível recuperar os dados originais a partir do hash.  
- Determinístico: a mesma entrada sempre gera o mesmo hash.

Algoritmos comuns:
- **SHA-256 / SHA-3:** padrão atual, seguro e resistente a colisões.  
- **MD5:** obsoleto, vulnerável a colisões; apenas para fins educacionais.  
- **bcrypt / Argon2:** projetados para armazenar senhas com proteção contra brute-force.

Uso típico:
- Armazenamento seguro de senhas.  
- Verificação de integridade de arquivos e downloads.  
- Criação de assinaturas digitais para autenticação e não-repúdio.

Exemplos práticos:
```bash
# Gerar hash SHA-256 de texto
echo "senha123" | sha256sum

# Gerar hash SHA-256 de arquivo
sha256sum arquivo.txt

# Comparar hash para verificar integridade
sha256sum -c arquivo.txt.sha256
