# 📖 Glossário – BlueTeam (Hackers do Bem)

Glossário organizado por categoria com os principais termos técnicos dos Módulos 1, 2 e 3.

---

## 🏗️ Arquitetura e Design de Rede

| Termo | Definição |
|-------|-----------|
| **ACL (Access Control List)** | Lista de regras que define quais pacotes são permitidos ou negados em um dispositivo de rede com base em IP, porta e protocolo. |
| **Balanceador de carga** | Dispositivo que distribui o tráfego entre vários servidores usando algoritmos como Round Robin, Least Connection ou Hashing. |
| **DMZ (Zona Desmilitarizada)** | Área isolada da rede onde ficam serviços públicos (web, e-mail, DNS). Fica entre dois firewalls, protegendo a rede interna. |
| **Firewall Stateful** | Firewall que analisa o estado da conexão, não apenas o cabeçalho. Sabe se um pacote faz parte de uma conexão legítima. |
| **IPv6** | Protocolo de internet com ~3,4×10³⁸ endereços. Formato: oito grupos de 4 dígitos hexadecimais separados por `:`. Suporte nativo a IPSec. |
| **MITM (Man-in-the-Middle)** | Ataque onde o invasor se posiciona entre dois dispositivos, interceptando e podendo modificar a comunicação. |
| **NAT (Network Address Translation)** | Traduz endereços IP internos para um IP público, escondendo a estrutura da rede interna. |
| **Segmentação de rede** | Divisão da rede em partes menores para limitar o impacto de ataques e dificultar movimentação lateral do invasor. |
| **STP (Spanning Tree Protocol)** | Protocolo que evita loops em redes de Camada 2 bloqueando links redundantes. Pode ser vulnerável a ataques com BPDU maliciosos. |
| **VLAN (Virtual Local Area Network)** | Segmentação lógica da rede física. Permite isolar departamentos, funções ou níveis de confiança na mesma infraestrutura. |

---

## 🛡️ Ataques e Defesa

| Termo | Definição |
|-------|-----------|
| **ARP Poisoning** | Ataque onde o invasor envia pacotes ARP falsos para associar seu MAC a um IP legítimo e interceptar o tráfego. |
| **DDoS (Distributed Denial of Service)** | Ataque que sobrecarrega um servidor ou serviço usando múltiplas fontes (botnet), tornando-o indisponível. |
| **IOC (Indicator of Compromise)** | Evidência forense que indica possível comprometimento (ex: endereço IP malicioso, hash de malware, padrão de tráfego). |
| **MAC Flooding** | Ataque que sobrecarrega a tabela CAM do switch, fazendo com que ele passe a funcionar como hub (envia pacotes para todas as portas). |
| **OSINT (Open Source Intelligence)** | Coleta e análise de informações disponíveis publicamente (redes sociais, sites, fóruns) para reconhecimento ou monitoramento. |
| **Phishing** | Técnica de engenharia social onde o atacante envia mensagens fraudulentas para enganar a vítima e obter informações sensíveis. |
| **Spoofing** | Falsificação de identidade (IP, MAC, e-mail) para se passar por dispositivo ou pessoa legítima. |
| **TTP (Tactics, Techniques, Procedures)** | Comportamento do atacante – suas táticas, técnicas e procedimentos. Usado para entender e mapear ameaças. |

---

## 🔐 Autenticação e Controle de Acesso

| Termo | Definição |
|-------|-----------|
| **2FA (Two-Factor Authentication)** | Autenticação que exige dois fatores diferentes (ex: senha + código do celular). |
| **Biometria** | Autenticação baseada em características únicas do usuário: impressão digital, reconhecimento facial, íris, voz. |
| **EAP (Extensible Authentication Protocol)** | Framework de autenticação usado em redes Wi-Fi e VPNs. Permite diferentes métodos (PEAP, EAP-TLS, EAP-TTLS). |
| **MFA (Multi-Factor Authentication)** | Autenticação que exige dois ou mais fatores (algo que você sabe, tem e/ou é). |
| **Princípio do Menor Privilégio** | Conceito de segurança onde usuários e processos recebem apenas os privilégios mínimos necessários para suas funções. |
| **RADIUS (Remote Authentication Dial-In User Service)** | Protocolo centralizado para autenticação, autorização e contabilidade (accounting). Muito usado em Wi-Fi corporativo e VPNs. |
| **TACACS+** | Protocolo de autenticação e autorização, com maior ênfase em controle de acesso. Encripta todo o pacote (diferente do RADIUS). |

---

## 🤖 Automação e Infraestrutura como Código

| Termo | Definição |
|-------|-----------|
| **Ansible** | Ferramenta de automação agentless (usa SSH). Playbooks em YAML. Desenvolvida pela RedHat. |
| **API (Application Programming Interface)** | Conjunto de regras e protocolos que permite a integração e comunicação entre diferentes sistemas. |
| **CI/CD (Continuous Integration/Continuous Deployment)** | Metodologias para integrar código continuamente e implantar automaticamente após testes. |
| **DevOps** | Cultura que une desenvolvimento e operações para promover colaboração, automação e entrega contínua. |
| **DevSecOps** | Extensão do DevOps que incorpora segurança em todas as etapas do ciclo de vida do desenvolvimento. |
| **IaC (Infrastructure as Code)** | Gerenciamento e provisionamento de infraestrutura por meio de código (arquivos de configuração versionáveis). |
| **Microsserviços** | Arquitetura onde os serviços são divididos em componentes menores e independentes, cada um com uma função específica. |
| **REST (Representational State Transfer)** | Abordagem arquitetural para construir APIs usando HTTP como base. Simples, escalável e interoperável. |
| **SOA (Service-Oriented Architecture)** | Arquitetura orientada a serviços baseada em serviços independentes que se comunicam por interfaces padronizadas. |
| **SOAR (Security Orchestration, Automation and Response)** | Tecnologia que automatiza tarefas de segurança (detecção, resposta, remediação) com inteligência artificial. |
| **SOAP (Simple Object Access Protocol)** | Protocolo de comunicação baseado em XML para troca de informações entre sistemas distribuídos. |
| **SAML (Security Assertion Markup Language)** | Linguagem de marcação para autenticação e autorização entre provedores de identidade e serviços (SSO). |

---

## 🔒 Criptografia e PKI

| Termo | Definição |
|-------|-----------|
| **AES (Advanced Encryption Standard)** | Algoritmo de criptografia simétrica amplamente usado, considerado seguro. Substituiu o DES. |
| **Assinatura digital** | Mecanismo que verifica autenticidade e integridade de um documento/mensagem usando criptografia assimétrica. |
| **Certificado digital** | Documento eletrônico que atesta a autenticidade de uma chave pública. Emitido por uma Autoridade Certificadora (CA). |
| **Criptografia assimétrica** | Usa um par de chaves: pública (criptografa) e privada (descriptografa). Ex: RSA, ECC. |
| **Criptografia simétrica** | Usa a mesma chave para criptografar e descriptografar. Ex: AES, DES. |
| **ECC (Elliptic Curve Cryptography)** | Criptografia assimétrica baseada em curvas elípticas. Oferece mesma segurança que RSA com chaves menores. |
| **Hashing** | Função unidirecional que transforma dados em uma sequência de tamanho fixo (hash). Ex: MD5 (inseguro), SHA-1 (inseguro), SHA-256 (seguro). |
| **PKI (Public Key Infrastructure)** | Infraestrutura de chave pública que gerencia certificados digitais, chaves e autoridades certificadoras. |
| **RSA (Rivest-Shamir-Adleman)** | Algoritmo de criptografia assimétrica amplamente usado para assinatura digital e troca de chaves. |
| **Salting** | Adição de uma sequência aleatória (salt) à senha antes do hash para impedir uso de rainbow tables. |
| **TPM (Trusted Platform Module)** | Chip de segurança dedicado que armazena chaves criptográficas e realiza operações seguras (assinatura, atestação). |

---

## 🖥️ Endpoint e Hardening

| Termo | Definição |
|-------|-----------|
| **BadUSB** | Ameaça onde o firmware de um dispositivo USB é modificado para executar ações maliciosas. |
| **DLP (Data Loss Prevention)** | Medidas para impedir cópia ou transferência não autorizada de dados confidenciais. |
| **EDR (Endpoint Detection and Response)** | Solução que monitora endpoints, registra eventos e permite investigação e resposta a incidentes. |
| **EPP (Endpoint Protection Platform)** | Plataforma que consolida proteção: antivírus, firewall, HIDS, criptografia, filtragem de conteúdo. |
| **FDE (Full Disk Encryption)** | Criptografia completa do disco. Exige autenticação (senha, TPM) para desbloquear os dados. |
| **Hardening** | Processo de redução da superfície de vulnerabilidade do sistema: desabilitar serviços, portas, aplicar patches. |
| **HIDS/HIPS** | Detecção e prevenção de intrusão baseada no próprio host. Monitora arquivos, rede e logs. |
| **SED (Self-Encrypting Drive)** | Unidade de armazenamento que faz criptografia no próprio hardware. Compatível com padrão Opal. |
| **Secure Boot** | Medida que verifica assinaturas digitais dos componentes do firmware antes da execução. |
| **Sheep dip** | Sistema sandbox para testar dispositivos USB novos ou suspeitos em ambiente isolado. |
| **UEFI (Unified Extensible Firmware Interface)** | Substitui o BIOS. Oferece recursos avançados como Secure Boot e verificação de integridade. |

---

## 📊 Logs, Monitoramento e SIEM

| Termo | Definição |
|-------|-----------|
| **DGA (Domain Generation Algorithm)** | Técnica usada por malware para gerar domínios dinamicamente, evitando listas negras estáticas. |
| **DMARC (Domain-based Message Authentication)** | Política que define como e-mails que falham SPF/DKIM devem ser tratados (quarentena, rejeição). |
| **DKIM (DomainKeys Identified Mail)** | Assinatura digital no cabeçalho do e-mail para verificar autenticidade e integridade. |
| **SIEM (Security Information and Event Management)** | Sistema que coleta, correlaciona e analisa eventos de segurança de múltiplas fontes para detecção de ameaças. |
| **SPF (Sender Policy Framework)** | Lista de endereços IP autorizados a enviar e-mails em nome de um domínio. |
| **Syslog** | Protocolo padrão para envio de logs. Formato: PRI (facility + severity), HEADER (timestamp + hostname), MSG (tag + conteúdo). |
| **Wireshark** | Ferramenta gráfica para captura e análise de pacotes de rede. Decodifica protocolos e permite filtros avançados. |
| **tcpdump** | Ferramenta CLI para captura de pacotes. Ampla usada em servidores Linux para troubleshooting e análise. |

---

## 🧠 Padrões e Frameworks

| Termo | Definição |
|-------|-----------|
| **CAPEC (Common Attack Pattern Enumeration and Classification)** | Catálogo de padrões de ataque comuns. Classifica e descreve como os ataques são realizados. |
| **CCE (Common Configuration Enumeration)** | Lista de configurações de segurança recomendadas para diferentes sistemas. |
| **CPE (Common Platform Enumeration)** | Nomenclatura padronizada para identificar plataformas de software e hardware. |
| **CVE (Common Vulnerabilities and Exposures)** | Identificador único para vulnerabilidades conhecidas. Ex: CVE-2024-12345. |
| **CVSS (Common Vulnerability Scoring System)** | Sistema de pontuação de vulnerabilidades (0 a 10). Composto por métricas: base, ambiental, temporal. |
| **CWE (Common Weakness Enumeration)** | Lista de fraquezas comuns em software e hardware. Ex: CWE-89 (SQL Injection). |
| **Cyber Kill Chain** | Modelo que descreve as etapas de um ataque cibernético (reconhecimento, invasão, exploração, etc.). |
| **MITRE ATT&CK** | Framework de conhecimento de adversários com táticas, técnicas e procedimentos (TTPs) reais. |

---

## 📡 Protocolos e Comunicação

| Termo | Definição |
|-------|-----------|
| **DNSSEC (Domain Name System Security Extensions)** | Extensão de segurança do DNS que adiciona assinaturas criptográficas aos registros, prevenindo envenenamento de cache. |
| **HTTPS (HTTP Secure)** | HTTP com SSL/TLS. Garante criptografia, autenticação do servidor e integridade dos dados. |
| **IKE (Internet Key Exchange)** | Protocolo usado na fase inicial do IPSec para negociar chaves e parâmetros de segurança. |
| **IPSec (Internet Protocol Security)** | Conjunto de protocolos que oferece autenticação, integridade e confidencialidade em redes IP. Componentes: ESP (criptografia) e AH (autenticação/integridade). |
| **mTLS (Mutual TLS)** | Extensão do TLS onde cliente e servidor se autenticam mutuamente. Usado em microserviços e zero trust. |
| **SFTP (Secure File Transfer Protocol)** | Transferência de arquivos segura usando SSH como transporte. |
| **SSH (Secure Shell)** | Protocolo para acesso remoto seguro. Substitui Telnet. Usa criptografia e autenticação por chave pública. |
| **SSL/TLS (Secure Sockets Layer / Transport Layer Security)** | Protocolos criptográficos para comunicação segura. TLS 1.2/1.3 são seguros; SSL e TLS 1.0/1.1 são obsoletos. |

---

## 🖥️ Redes sem Fio (Wi-Fi)

| Termo | Definição |
|-------|-----------|
| **802.11ax (Wi-Fi 6)** | Padrão Wi-Fi mais recente. Opera em 2,4 e 5 GHz. Velocidade até 9,6 Gbps. Suporte a WPA3. |
| **SSID (Service Set Identifier)** | Nome da rede Wi-Fi. Pode ser oculto (não recomendado como única medida de segurança). |
| **WEP (Wired Equivalent Privacy)** | Protocolo de segurança Wi-Fi obsoleto e inseguro. Não deve ser usado. |
| **WPA (Wi-Fi Protected Access)** | Protocolo que substituiu o WEP. Usava TKIP. Vulnerável e obsoleto. |
| **WPA2 (Wi-Fi Protected Access 2)** | Padrão atual. Usa AES-CCMP. Modos: Personal (PSK) e Enterprise (EAP/RADIUS). |
| **WPA3 (Wi-Fi Protected Access 3)** | Padrão mais recente. Usa SAE (autenticação individualizada) e AES-GCMP. Proteção contra força bruta offline. |

---

## 📦 Virtualização e Nuvem

| Termo | Definição |
|-------|-----------|
| **Hypervisor Tipo 1 (Bare-metal)** | Executa diretamente no hardware. Ex: VMware ESXi, KVM, Hyper-V. Melhor desempenho. |
| **Hypervisor Tipo 2 (Hosted)** | Executa como aplicativo sobre um SO existente. Ex: VirtualBox, VMware Workstation. |
| **KVM (Kernel-based Virtual Machine)** | Hypervisor tipo 1 nativo do Linux. Usado com QEMU para virtualização. |
| **Snapshot** | Captura do estado de uma VM em um momento específico. Útil para recuperação rápida, mas não substitui backup. |
| **VM escape** | Vulnerabilidade onde o invasor "fura" a VM e acessa o hypervisor ou outras VMs. |

---

## 🏭 Sistemas Embarcados e Industrial (OT/SCADA)

| Termo | Definição |
|-------|-----------|
| **FPGA (Field-Programmable Gate Array)** | Chip que pode ser configurado pelo cliente final para lógica de programação personalizada. |
| **HMI (Human-Machine Interface)** | Interface entre humanos e máquinas em sistemas industriais. Deve ter controles de acesso seguros. |
| **ICS (Industrial Control System)** | Sistemas usados para automatizar processos industriais (usinas, plantas químicas). |
| **NB-IoT (Narrowband IoT)** | Tecnologia de comunicação de baixa potência e longo alcance para dispositivos IoT. |
| **OT (Operational Technology)** | Redes e sistemas usados em ambientes industriais (diferente de TI tradicional). |
| **PLC (Programmable Logic Controller)** | Controlador lógico programável usado em sistemas embarcados industriais. |
| **RTOS (Real-Time Operating System)** | Sistema operacional de tempo real que prioriza tarefas críticas e alta estabilidade. |
| **SCADA (Supervisory Control and Data Acquisition)** | Sistema para monitoramento e controle de processos industriais. Executado em sistemas embarcados. |
| **SoC (System on a Chip)** | Processador, controladores e dispositivos em um único pacote (ex: Raspberry Pi, Arduino). |
| **Zigbee** | Protocolo para comunicação sem fio de baixa potência em 2,4 GHz. Usado em automação residencial e IoT. |
| **Z-Wave** | Protocolo para comunicação sem fio de baixa potência em ~900 MHz. Usado em automação residencial. |

---

## 🪟 Sistemas Operacionais (Windows/Linux)

| Termo | Definição |
|-------|-----------|
| **OpenLDAP** | Serviço de diretório open source para autenticação centralizada em ambientes Linux. |
| **PowerShell** | Ferramenta de automação e gerenciamento de tarefas no Windows (linha de comando + scripting). |
| **WSUS (Windows Server Update Services)** | Serviço da Microsoft para gerenciamento centralizado de atualizações em ambientes Windows. |

---

## ⚠️ Legislação e Compliance

| Termo | Definição |
|-------|-----------|
| **GDPR (General Data Protection Regulation)** | Regulamento da União Europeia para proteção de dados pessoais. |
| **LGPD (Lei Geral de Proteção de Dados)** | Lei brasileira para tratamento de dados pessoais (semelhante ao GDPR). |
| **Marco Civil da Internet** | Lei brasileira que estabelece princípios, garantias e deveres para o uso da internet. |
| **PCI DSS (Payment Card Industry Data Security Standard)** | Padrão internacional para segurança de dados de cartões de pagamento. |