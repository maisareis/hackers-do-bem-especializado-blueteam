# Aula 2 – Ataques e Estratégias de Defesa

## 📌 Contexto Global
Os ciberataques estão entre os maiores riscos globais segundo o Fórum Econômico Mundial (relatórios de 2022 e 2023). O Brasil lidera em callbacks de APTs na América Latina.

**Evolução do foco em segurança:**
- Anos 90 → prevenção
- Anos 2000 → detecção
- Hoje → **resposta**

---

## 📌 Vulnerabilidade, Ameaça e Risco
- **Vulnerabilidade** = fraqueza no sistema (ex: porta aberta sem necessidade)
- **Ameaça** = quem ou o que pode explorar essa fraqueza
- **Risco** = probabilidade de uma ameaça explorar a vulnerabilidade × impacto se isso acontecer

---

## 📌 Tipos de Atores de Ameaça

| Ator | Características |
|------|----------------|
| **Hacker** | Alta habilidade técnica; pode ser ético ou malicioso |
| **Script Kiddie** | Usa ferramentas prontas sem entender o que está fazendo; busca emoção e notoriedade |
| **Hacktivista** | Motivação política, social ou ideológica; deface, DDoS, vazamentos |
| **Ator Estatal** | Recursos elevados; espionagem, sabotagem de infraestrutura crítica |
| **APT** | Ameaça Persistente Avançada: altamente habilidosa, patrocinada, foca em alvos de alto valor, fica meses sem ser detectada |
| **Sindicato Criminoso** | Fins financeiros: ransomware, fraude, tráfico de dados |
| **Ameaça Interna** | Funcionário, ex-funcionário ou prestador com acesso legítimo; risco elevado por já estar dentro |
| **Competidor** | Espionagem industrial, roubo de propriedade intelectual |

**Callback (APT):** canal de comunicação oculto entre o sistema comprometido e o servidor do atacante. Usa protocolos cifrados (ex: HTTPS) para passar despercebido por firewalls e IDS. É o que mantém o controle remoto mesmo depois da infecção inicial.

---

## 📌 Vetores de Ataque

| Vetor | Como funciona |
|-------|---------------|
| **Acesso Direto** | Acesso físico ao dispositivo (USB, porta de rede) |
| **Mídia Removível** | Pendrive ou HD externo infectado com malware |
| **E-mail** | Phishing, spear phishing, anexos maliciosos |
| **Acesso Remoto / Wi-Fi** | VPN comprometida, senhas fracas, Wi-Fi público sem criptografia |
| **Cadeia de Suprimentos** | Comprometimento de fornecedores ou componentes de software/hardware |
| **Web / Redes Sociais** | XSS, injeção de código, engenharia social, links maliciosos |
| **Nuvem** | Credenciais vazadas, configurações incorretas, injeção em serviços cloud |

---

## 📌 Fontes de Inteligência de Ameaças

**OSINT (Open Source Intelligence):**
Coleta de informações em fontes públicas (sites, redes sociais, fóruns, registros públicos). No Blue Team é usada para:
- Descobrir quais ativos da organização estão expostos na internet
- Criar perfis de possíveis atacantes
- Monitorar vazamentos de dados
- Identificar vulnerabilidades conhecidas antes do atacante

**Outras fontes:**
- Comunidades de segurança e fóruns especializados
- Relatórios de incidentes (IBRASPD, CERT.br)
- Redes de compartilhamento de IoC (Indicadores de Comprometimento)
- **The DFIR Report** → análises detalhadas de incidentes reais com TTPs mapeadas

**TTPs (Táticas, Técnicas e Procedimentos):** descrevem como o atacante opera em cada fase do ataque.

**IoCs:** evidências de comprometimento – endereços IP, URLs, hashes de arquivos, padrões de tráfego, assinaturas de malware.

---

## 📌 Tipos de Controles de Segurança

**Por categoria:**
- **Administrativo** → políticas, procedimentos, treinamentos
- **Técnico** → firewalls, antivírus, criptografia
- **Físico** → câmeras, catracas, controle de acesso a salas

**Por função:**
- **Preventivo** → evita que o incidente aconteça (ex: firewall, MFA)
- **Detectivo** → identifica incidentes em andamento (ex: IDS, SIEM)
- **Corretivo** → restaura a normalidade após o incidente (ex: backup, IRP)
- **Dissuasor** → desencoraja o ataque (ex: aviso de monitoramento)
- **Compensatório** → substitui um controle principal que não pode ser aplicado

---

## 📌 Frameworks de Segurança

**NIST Cybersecurity Framework:** Identificar → Proteger → Detectar → Responder → Recuperar

**MITRE ATT&CK:** base de conhecimento de táticas e técnicas usadas por adversários reais, organizada por fases do ataque.

**Cyber Kill Chain:** modelo de 7 etapas de um ataque cibernético.

| Etapa | O que acontece |
|-------|----------------|
| Reconhecimento | Coleta de informações sobre o alvo |
| Weaponização | Criação da arma (malware + exploit) |
| Entrega | Envio da arma (e-mail, USB, site) |
| Exploração | Execução do exploit na máquina alvo |
| Instalação | Malware se instala para persistência |
| C2 (Comando e Controle) | Atacante assume controle remoto |
| Ações | Objetivo final: roubo, destruição, ransomware |

**ISO 27001/27002:** normas para gestão de segurança da informação.

**CIS Benchmarks:** guias de configuração segura para sistemas e aplicativos.

**LGPD / GDPR:** legislações que regulam coleta, armazenamento e uso de dados pessoais.

---

## 💡 Meus Insights
- **Ameaça interna:** É o vetor que mais me impressionou. O atacante já tem as credenciais, já conhece os sistemas, já sabe onde estão os dados sensíveis. Muito mais difícil de detectar que um ataque externo.
- **Kill Chain:** Entendi que se o Blue Team consegue interromper o ataque em qualquer etapa antes da fase de C2, o dano é muito menor. A ideia de "defesa em camadas" faz muito sentido aqui.
- **OSINT:** Percebi que o Blue Team usa OSINT de forma defensiva – para enxergar o que o atacante veria antes dele ver. Proatividade é a chave.
- **TTPs vs IoCs:** IoCs ficam desatualizados rápido (IPs mudam, hashes são alterados). TTPs são mais estáveis porque atacantes reutilizam técnicas mesmo mudando de ferramentas.
- **Dúvida:** Como uma empresa pequena, sem SOC, consegue aplicar threat intelligence na prática?
