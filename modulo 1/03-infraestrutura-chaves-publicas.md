# Aula 3 – Infraestrutura de Chaves Públicas

## 📌 Criptografia: o básico
Técnica que transforma dados em algo ilegível para quem não tem a chave de decodificação. Garante confidencialidade, integridade e autenticidade.

**Dois tipos principais:**

| Tipo | Como funciona | Exemplos |
|------|--------------|----------|
| **Simétrica** | Mesma chave para cifrar e decifrar | AES, DES |
| **Assimétrica** | Par de chaves: pública (cifra) e privada (decifra) | RSA, ECC |

A simétrica é mais rápida, mas exige compartilhamento seguro da chave. A assimétrica resolve isso – a chave pública pode ser distribuída livremente.

---

## 📌 Algoritmos de Hashing
Transformam qualquer dado em uma sequência fixa de caracteres (o hash). Características:
- **Unidirecional** → não dá pra obter o dado original a partir do hash
- **Determinístico** → mesmo dado sempre gera mesmo hash
- **Efeito avalanche** → qualquer alteração mínima muda o hash completamente

**Usos:** verificação de integridade de arquivos, armazenamento seguro de senhas, assinaturas digitais.

| Algoritmo | Situação |
|-----------|----------|
| MD5 | Frágil – não usar para segurança |
| SHA-1 | Frágil – não recomendado |
| SHA-256 | Seguro – amplamente adotado |

---

## 📌 Outros Conceitos Criptográficos

**Cifras de fluxo vs. cifras de bloco:**
- **Fluxo** → cifra bit a bit (ex: RC4)
- **Bloco** → divide os dados em blocos e cifra cada um (ex: AES, DES)

**Envelope digital:** solução para o problema de troca de chaves na criptografia assimétrica. A chave de sessão (simétrica) é cifrada com a chave pública do destinatário e enviada junto com a mensagem cifrada.

**Assinatura digital:** usa a chave privada do remetente para assinar e a chave pública para verificar. Garante autenticidade e não repúdio.

**Modos de operação autenticados:** além de cifrar, também garantem integridade (ex: GCM, CCM).

**Colisão e ataque do aniversário:** colisão é quando dois dados diferentes geram o mesmo hash. O ataque do aniversário explora a probabilidade estatística de encontrar essa colisão em grandes conjuntos de dados.

---

## 📌 PKI – Infraestrutura de Chave Pública
Sistema que organiza o uso de criptografia assimétrica com certificados digitais e autoridades certificadoras.

**Autoridade Certificadora (AC/CA):**
- Emite e assina digitalmente os certificados
- Verifica a identidade de quem solicita um certificado
- É reconhecida como confiável pelos navegadores e sistemas

**Cadeia de certificados:** hierarquia de CAs. Para validar um certificado, sobe-se a cadeia até chegar na CA raiz confiável.

**CSR (Certificate Signing Request):** pedido de assinatura de certificado. Contém nome, chave pública e outros dados da entidade que quer o certificado.

**Tipos de certificado:**

| Tipo | Uso |
|------|-----|
| SSL/TLS (Single Domain) | Um domínio |
| Multi-Domain | Vários domínios no mesmo certificado |
| Wildcard | Domínio principal + todos os subdomínios |
| Assinatura Digital | Validar autoria de documentos |
| Código | Autenticidade de software |

**Revogação:**
- **CRL (Certificate Revocation List)** → lista de certificados revogados antes do prazo
- **OCSP** → consulta em tempo real se o certificado está válido ou revogado

---

## 📌 HSTS (HTTP Strict Transport Security)
Mecanismo que obriga o navegador a usar HTTPS em todas as conexões com um site, mesmo que o usuário tente acessar via HTTP. Protege contra ataques de downgrade e MITM.

---

## 📌 Formatos e Ferramentas

| Item | Descrição |
|------|-----------|
| **X.509** | Padrão de formato de certificados digitais |
| **PEM** | Formato ASCII para certificados e chaves |
| **OpenSSL** | Biblioteca open source para criptografia e gestão de certificados |

---

## 💡 Meus Insights
- **Chave pública vs. privada:** A analogia que ficou pra mim: a chave pública é o cadeado (qualquer um pode usar para trancar), a chave privada é a chave (só o dono consegue abrir).
- **PKI na prática:** Toda vez que vejo o cadeado verde no navegador, é a PKI funcionando – a CA validou aquele servidor e o navegador confia na CA. A cadeia de confiança é invisível mas está sempre lá.
- **SHA-256 vs MD5:** MD5 já foi quebrado. SHA-1 também. Usando hoje para qualquer coisa séria tem que ser SHA-256 no mínimo.
- **HSTS:** Simples mas eficaz. Uma única linha de configuração no servidor que elimina um vetor de ataque inteiro.
- **Dúvida:** Em ambientes onde não dá para usar uma CA pública (sistema fechado, rede interna), como funciona a cadeia de confiança com uma CA privada?
