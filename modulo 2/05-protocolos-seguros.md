# 🔒 Aula 5 – Protocolos Seguros de Rede

## 📌 Conceitos-chave

- HTTPS: HTTP + SSL/TLS, criptografia, autenticação de servidor, integridade
- SSH: acesso remoto seguro, substitui Telnet, autenticação por chave pública
- SFTP: transferência de arquivos sobre SSH
- DNSSEC: assinaturas criptográficas no DNS, evita envenenamento de cache
- SSL/TLS: handshake, certificados, chave de sessão
- mTLS: autenticação mútua (cliente e servidor)
- IPSec: ESP (criptografia), AH (autenticação/integridade), modos transporte e túnel
- IKE: Internet Key Exchange – fases 1 e 2 para estabelecer túneis IPSec

## 📌 Resumo da aula

### HTTPS

| Benefício | Descrição |
|-----------|-----------|
| Criptografia | Dados ilegíveis durante a transmissão |
| Autenticação do servidor | Certificado digital verifica identidade do site |
| Integridade | Detecta modificação dos dados em trânsito |
| Confiança do usuário | Cadeado na barra de endereço |

### SSH (Secure Shell)

**Handshake SSH:**
1. Cliente e servidor trocam versões e algoritmos suportados
2. Negociação de algoritmos (criptografia, MAC, compressão)
3. Diffie-Hellman para troca de chaves
4. Servidor envia certificado/chave pública
5. Cliente autentica (senha ou chave pública)
6. Conexão segura estabelecida

### SFTP

- Transferência de arquivos segura usando SSH como transporte
- Autenticação, criptografia e integridade herdadas do SSH
- Boas práticas: autenticação por chave pública, gerenciamento de chaves, configurar servidor seguro

### DNSSEC

**Problema do DNS tradicional:** envenenamento de cache, spoofing, interceptação

**Solução DNSSEC:**
- Adiciona assinaturas criptográficas aos registros DNS
- RRsets (Resource Record sets) – agrupa registros do mesmo tipo
- ZSK (Zone Signing Key) – assina os RRsets
- KSK (Key Signing Key) – assina a ZSK
- Cadeia de confiança – da zona raiz até o domínio

### SSL/TLS

| Versão | Característica |
|--------|----------------|
| SSL 2.0/3.0 | Obsoletos, inseguros |
| TLS 1.0/1.1 | Descontinuados |
| TLS 1.2 | Amplamente usado |
| TLS 1.3 | Mais rápido e seguro |

**Handshake TLS:**
1. Cliente solicita conexão segura
2. Servidor envia certificado com chave pública
3. Cliente valida certificado
4. Cliente gera chave de sessão, criptografa com chave pública do servidor
5. Servidor descriptografa com chave privada
6. Comunicação segue com criptografia simétrica (mais eficiente)

### mTLS (Mutual TLS)

- Cliente e servidor se autenticam mutuamente
- Organização atua como sua própria Autoridade Certificadora (CA)
- Certificado raiz autoassinado interno
- Usado em microserviços, APIs internas, zero trust

### IPSec

**Componentes:**
| Componente | Função |
|------------|--------|
| ESP (Encapsulating Security Payload) | Criptografia (confidencialidade) |
| AH (Authentication Header) | Autenticação e integridade (sem criptografia) |

**Modos de operação:**
- **Transporte:** só a carga útil é criptografada (IP original visível)
- **Túnel:** pacote IP inteiro é encapsulado e criptografado

### IKE (Internet Key Exchange)

**Fase 1:** estabelece canal seguro para negociação (autenticação, troca de chaves Diffie-Hellman, SA inicial)

**Fase 2:** negocia parâmetros específicos do IPSec (endereços, portas, algoritmos para o túnel)

## 💡 Meus Insights

**HTTPS não é opção, é obrigação:** Em 2024, site sem HTTPS é irresponsável. O cadeado não é só segurança, é credibilidade. Usuário já foi treinado pra desconfiar de site sem cadeado.

**SSH matou o Telnet com razão:** Telnet manda senha em texto puro. Num mesmo switch, qualquer um com Wireshark pega. SSH é tão simples de configurar que não tem desculpa.

**Chave pública vs senha no SSH:** Senha SSH é melhor que Telnet, mas chave pública é outro nível. Sem senha pra brute force, e você ainda pode proteger a chave com passphrase. O chato é gerenciar as chaves, mas a segurança compensa.

**DNSSEC é necessário mas ninguém implementa:** Todo mundo reclama de spoofing de DNS, mas DNSSEC exige esforço. A cadeia de confiança é elegante tecnicamente, mas na prática, poucas zonas são assinadas. O problema é que o modelo atual ainda depende da boa vontade do administrador.

**TLS 1.3 é mais rápido e mais seguro:** Removeram os algoritmos ruins e reduziram o handshake de 2 viagens (1.2) para 1 (1.3). Menos tempo de conexão = melhor performance.

**mTLS é o futuro do zero trust:** Em vez de confiar só na senha ou no certificado do servidor, mTLS exige que o cliente também prove quem é. Perfeito para microserviços onde máquinas se comunicam sem humano no meio.

**IPSec ainda vive (e bem):** Em VPNs site-to-site (empresa-filial), IPSec continua sendo o padrão. OpenSSL é ótimo, mas IPSec no modo túnel entre firewalls é robusto, testado e funciona em qualquer equipamento minimamente decente.

**Fases IKE:** A Fase 1 é mais lenta (usa criptografia assimétrica), mas estabelece o túnel seguro pra Fase 2 ser rápida. É o mesmo princípio do TLS: faz a negociação pesada uma vez, depois usa chave simétrica pro resto.