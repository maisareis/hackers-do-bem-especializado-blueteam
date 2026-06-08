# 🔑 Aula 3 – Técnicas de Autenticação

## 📌 Conceitos-chave

- Autenticação: verificação da identidade de um usuário ou sistema
- Três fatores de autenticação: algo que você sabe (senha), algo que você tem (token), algo que você é (biometria)
- Autenticação de senha: melhores práticas, hashing, salting, gerenciadores de senhas
- Autenticação de dois fatores (2FA) e multifator (MFA)
- Autenticação biométrica: impressão digital, facial, íris, voz
- Tokens de autenticação: hardware (USB, smart card) e software (aplicativos móveis)
- Protocolos de autenticação de rede: RADIUS, TACACS+, EAP, Kerberos, LDAP, SAML
- WPA2-Enterprise: autenticação baseada em EAP/RADIUS para redes Wi-Fi
- Autenticação em nuvem: Azure AD, AWS IAM, Google Cloud IAM
- Gerenciamento de Identidade e Acesso (IAM): provisionamento, RBAC, princípio do menor privilégio
- Tendências: autenticação baseada em contexto e zero trust

## 📌 Resumo da aula

### Os Três Fatores de Autenticação

| Fator | Exemplo | Descrição |
|-------|---------|-----------|
| Algo que você sabe | Senha, PIN, resposta a pergunta secreta | Informação memorizada |
| Algo que você tem | Token USB, smart card, celular, aplicativo autenticador | Objeto físico ou dispositivo |
| Algo que você é | Impressão digital, reconhecimento facial, íris, voz | Característica biométrica inerente |

### Autenticação por Senha

**Melhores práticas:**
- Comprimento mínimo: 12 caracteres
- Complexidade: maiúsculas, minúsculas, números, caracteres especiais
- Evitar informações pessoais e sequências óbvias
- Não reutilizar senhas entre serviços
- Troca periódica (a cada 60-90 dias)
- Autenticação de dois fatores (2FA) sempre que disponível

**Proteção de senhas armazenadas:**

| Método | Descrição |
|--------|-----------|
| Criptografia | Transforma senha em formato ilegível |
| Hashing | Gera sequência única e irreversível (bcrypt, PBKDF2, scrypt) |
| Salting | Adiciona sequência aleatória antes do hash (impede rainbow tables) |

**Quanto tempo para quebrar uma senha (8 caracteres):**
- Só números: instantâneo
- Minúsculas: 22 minutos
- Maiúsculas + minúsculas: 1 hora
- Maiúsculas + minúsculas + números + símbolos: 8 horas

### Autenticação de Dois Fatores (2FA) e Multifator (MFA)

**Benefícios:**
- Mesmo com senha comprometida, segundo fator impede acesso
- Redução significativa de fraudes e sequestro de contas
- Exigido por regulamentações em muitos setores

**Segundo fator comum:**
- Código via SMS
- Aplicativo autenticador (Google Authenticator, Microsoft Authenticator)
- Token físico (YubiKey)
- Biometria como segundo fator
- Notificação push no celular

### Autenticação Biométrica

**Tipos de biometria:**
- Impressão digital
- Reconhecimento facial
- Íris
- Voz
- Dinâmica de digitação (comportamental)

**Vantagens:**
- Identificação precisa (características únicas)
- Conveniente (não precisa memorizar)
- Difícil de falsificar

**Desafios:**
- Privacidade e proteção de dados (LGPD, GDPR)
- Variação em diferentes condições (iluminação, qualidade do sensor)
- Custo de implementação
- Aceitação do usuário

**Armazenamento seguro de dados biométricos:**
- Criptografia forte
- Chaves de criptografia robustas
- Consentimento explícito do usuário
- Anonimização e minimização dos dados

### Tokens de Autenticação

| Tipo | Exemplos | Característica |
|------|----------|----------------|
| Hardware | Token USB, smart card, leitor de impressão digital | Físico, portátil, durável, seguro |
| Software | Google Authenticator, Microsoft Authenticator, Authy | Aplicativo no celular/computador |

### Protocolos de Autenticação de Rede

| Protocolo | Função | Característica |
|-----------|--------|----------------|
| RADIUS | Autenticação, autorização e contabilidade | Centralizado, para redes de grande porte |
| TACACS+ | Autenticação e autorização | Maior ênfase em controle de acesso, várias etapas |
| EAP | Framework de autenticação flexível | Usado em Wi-Fi e VPNs (PEAP, EAP-TLS, EAP-TTLS) |
| Kerberos | Autenticação em redes Windows | Baseado em tickets, sem envio de senha pela rede |
| LDAP | Acesso a serviços de diretório | Consulta e autenticação em diretórios (ex: OpenLDAP) |
| SAML | Autenticação federada | SSO entre diferentes domínios/serviços |

### WPA2-Enterprise

**Diferencial em relação ao WPA2-Personal:**
- Autenticação individual por usuário/dispositivo (não apenas pela senha da rede)
- Servidor RADIUS centralizado
- Certificados digitais (EAP-TLS, PEAP)
- Segurança muito superior para ambientes corporativos

**Fluxo básico:**
1. Dispositivo tenta se conectar ao AP
2. AP encaminha autenticação para servidor RADIUS
3. Servidor valida credenciais (usuário/senha ou certificado)
4. Acesso concedido ou negado

### Autenticação em Nuvem

| Provedor | Serviço de IAM | Recursos |
|----------|----------------|----------|
| Microsoft Azure | Azure Active Directory (AD) | SSO, RBAC, sincronização com AD local |
| Amazon AWS | AWS Identity and Access Management (IAM) | Políticas de acesso, roles temporárias |
| Google Cloud | Google Cloud IAM | RBAC, auditoria, políticas granulares |

### Gerenciamento de Identidade e Acesso (IAM) em Nuvem

**Elementos essenciais:**
- Provisionamento e desprovisionamento automático de contas
- Sincronização de identidades com diretório local
- Políticas rigorosas de gerenciamento de senhas
- Controle de acesso baseado em função (RBAC)
- Monitoramento contínuo e auditoria
- Princípio do menor privilégio

### Tendências Emergentes

**Autenticação baseada em contexto:**
- Avalia localização, horário, tipo de dispositivo, comportamento do usuário, nível de risco
- Ajusta a rigidez da autenticação com base no contexto

**Autenticação Zero Trust:**
- "Nunca confie, sempre verifique"
- Não há confiança implícita (nem dentro da rede)
- Verificação contínua e baseada em fatores de risco
- Requer mudança cultural e infraestrutura robusta

## 💡 Meus Insights

**Senha forte é o mínimo, não é o suficiente:** A tabela de tempo de quebra mostra que 8 caracteres comuns são quebrados em horas. 12 caracteres complexos já são anos, mas ainda assim, senha sozinha é risco. 2FA não é opcional para serviços críticos.

**Gerenciador de senhas resolve o problema da reutilização:** O usuário comum não consegue lembrar 30 senhas complexas. Por isso repete "Senha123" em tudo. Gerenciador de senhas (Bitwarden, 1Password, Keepass) resolve isso. Educar o usuário para usar um deveria ser prioridade.

**MFA não é invencível, mas é muito bom:** Sim, MFA pode ser contornado (SIM swap, phishing de sessão). Mas eleva o custo do ataque tanto que a maioria dos invasores parte para alvos mais fáceis. Para o usuário comum, MFA já é proteção suficiente.

**Biometria é conveniente, não mais segura:** Impressão digital é prática, mas não é segredo. Sua digital está em todo lugar (maçaneta, copo, tela do celular). É boa como segundo fator, mas não como fator único.

**WPA2-Enterprise é o padrão corporativo:** Em qualquer empresa com mais de 50 funcionários, usar PSK (senha compartilhada) é insustentável. WPA2-Enterprise com RADIUS permite que cada usuário tenha sua própria senha, que pode ser revogada individualmente. E ainda integra com Active Directory ou LDAP.

**RADIUS vs TACACS+:** RADIUS é mais comum em Wi-Fi e VPN, encripta só a senha. TACACS+ encripta todo o pacote e separa autenticação de autorização. Em equipamentos de rede (Cisco, Huawei), TACACS+ é preferido.

**Kerberos é elegante, mas exige sincronização de tempo:** O protocolo de tickets é seguro e não envia senha pela rede. Mas depende de relógios sincronizados (NTP) e infraestrutura de chaves bem cuidada.

**SSO facilita a vida e aumenta segurança (se bem feito):** Single Sign-On reduz fadiga de senha e permite políticas centralizadas. Mas o ponto único de falha (Identity Provider) vira alvo principal. Proteger esse ponto com MFA e monitoramento é crítico.

**Zero trust não é hype:** A ideia de não confiar em nada, nem dentro da rede, é necessária com o fim do perímetro tradicional. Autenticação contínua, não só no login, é o caminho.