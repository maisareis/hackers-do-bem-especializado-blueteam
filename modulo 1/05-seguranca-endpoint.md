# Aula 5 – Segurança no Endpoint

## 📌 Firmware Seguro

**O que é firmware:** software embarcado nos dispositivos que controla o hardware. Presente em roteadores, impressoras, placas-mãe, smart TVs e praticamente qualquer eletrônico.

**Hardware Root of Trust (Âncora de Confiança):**
Componente de hardware confiável (ex: chip de segurança) que verifica a integridade do firmware durante a inicialização. Garante que só software autorizado execute.

**TPM (Trusted Platform Module):** chip dedicado que armazena chaves criptográficas e realiza operações de autenticação. É a implementação mais comum de Root of Trust.

---

## 📌 Integridade de Inicialização (Boot)

**UEFI:** substituto moderno do BIOS. Suporta recursos avançados de segurança.

| Mecanismo | O que faz |
|-----------|-----------|
| **Secure Boot** | Verifica assinaturas digitais dos componentes antes de executar |
| **Measured Boot** | Usa o TPM para medir e registrar o hash de cada etapa da inicialização |
| **Boot Attestation** | Envia relatório de integridade para um servidor remoto para auditoria |

---

## 📌 Criptografia de Armazenamento

**FDE (Full Disk Encryption):** cifra todo o conteúdo do disco. Sem a senha/chave, os dados são inacessíveis mesmo com acesso físico ao dispositivo. A chave pode ser protegida por senha do usuário, TPM ou dispositivo USB externo.

**SED (Self-Encrypting Drive):** o próprio disco faz a criptografia em hardware. Usa DEK/MEK (chave de dados) + AK/KEK (chave de autenticação). Compatível com o padrão Opal.

---

## 📌 Segurança em Dispositivos USB

**BadUSB:** firmware malicioso em dispositivos USB. Um pendrive aparentemente normal pode conter código que infecta o sistema, rouba dados ou assume controle remoto.

**Sheep Dip:** sistema de sandbox isolado (sem conexão com a rede de produção) usado para analisar dispositivos USB suspeitos antes de conectar em sistemas reais.

**Boas práticas:**
- Nunca conectar dispositivos USB de origem desconhecida em sistemas importantes
- Manter SO e antivírus atualizados
- Usar soluções que detectem e bloqueiem BadUSB em tempo real

---

## 📌 Hardening de Endpoint

Reduzir a superfície de ataque do dispositivo:
- Desativar serviços e portas desnecessárias
- Gerenciar as portas TCP/UDP abertas via firewall
- Criptografar o armazenamento persistente
- Usar GPOs (Group Policy Objects) para aplicar configurações seguras em massa
- Monitorar desvios da configuração baseline (linha de base)

**Gerenciamento de patches:** vulnerabilidades surgem constantemente. Ter um cronograma de atualização é essencial. Para sistemas legados que não recebem mais suporte, compensar com outras medidas (segmentação, monitoramento reforçado).

---

## 📌 Soluções de Proteção de Endpoint

| Solução | O que faz |
|---------|-----------|
| **Antivírus/Antimalware** | Detecta malware por assinatura e heurística |
| **HIDS/HIPS** | Monitora integridade de arquivos e tráfego no próprio dispositivo |
| **EPP (Endpoint Protection Platform)** | Consolida antivírus, firewall, DLP e criptografia num único agente |
| **EDR (Endpoint Detection and Response)** | Visibilidade avançada + contenção; usa ML para detectar comportamentos anômalos |
| **DLP (Data Loss Prevention)** | Impede cópia ou transferência não autorizada de dados sensíveis |
| **Sandbox** | Executa arquivos suspeitos em ambiente isolado para análise segura |

**DLP – Maturidade em 4 estágios:**
1. Descoberta e classificação da informação + políticas de prevenção
2. Identificação de processos de negócio e avaliação de gaps
3. Implementação tecnológica e revisão de conformidade
4. Remediação e governança contínua

~83% das organizações já sofreram algum tipo de violação de dados.

---

## 📌 Gerenciamento de Risco de Terceiros

A cadeia de suprimentos é um vetor de ataque real. Componentes de hardware ou software comprometidos podem introduzir backdoors antes mesmo de chegarem à organização.

**EOL (End of Life):** produto não está mais disponível para novos clientes; peças e atualizações podem escassear.

**EOSL (End of Service Life):** fabricante encerra o suporte completamente. Sem patches de segurança. Sem suporte técnico.

**Abandonware:** produto completamente abandonado pelo fabricante. Alto risco.

**O que fazer com sistemas sem suporte:** segmentar a rede, reforçar o monitoramento, implementar controles compensatórios.

---

## 📌 Sistemas Embarcados e ICS

**Sistemas embarcados:** desenvolvidos para função específica (ex: controlador industrial, dispositivo médico, veículo). Operam em ambientes estáticos com recursos limitados de processamento e energia.

**Desafios de segurança:**
- Recursos limitados para criptografia robusta
- Ausência de Root of Trust
- Conectados à rede, mas sem as medidas de segurança de sistemas de propósito geral

**ICS (Industrial Control Systems):** automatizam processos industriais. Componentes:

| Componente | Função |
|------------|--------|
| **PLC** | Controlador lógico programável |
| **SoC** | Sistema em um chip (Raspberry Pi, Arduino) |
| **FPGA** | Lógica de programação configurável pelo cliente |
| **RTOS** | Sistema operacional de tempo real |
| **SCADA** | Supervisão e aquisição de dados de processos industriais |
| **HMI** | Interface humano-máquina |

**SCADA:** vulnerável a ataques cibernéticos por estar conectado à rede. Medidas essenciais: segmentação de rede e autenticação robusta.

**Protocolos IoT de baixa potência:**
- **Z-Wave** → ~900 MHz
- **Zigbee** → 2,4 GHz
- **NB-IoT** → celular, baixo consumo
- **LTE-M** → celular, baixa latência

---

## 💡 Meus Insights
- **BadUSB:** Assustador porque é invisível. O sistema operacional vê um dispositivo USB normal. A ameaça está no firmware, não no arquivo. Não tem como saber olhando pro pendrive.
- **EDR vs antivírus:** Antivírus reage a assinaturas conhecidas. EDR analisa comportamento – consegue pegar ameaças novas que ainda não têm assinatura. Para Blue Team, EDR é muito mais relevante.
- **SCADA:** A convergência entre OT (tecnologia operacional) e IT (tecnologia da informação) criou um problema enorme. Sistemas industriais foram projetados para funcionar em redes isoladas. Quando conectam à internet, ficam expostos sem ter as defesas adequadas.
- **EOL/EOSL:** Na prática de suporte eu já vi isso acontecer – sistema legado sem patch, sem suporte, e a empresa simplesmente não consegue migrar por causa do custo ou da criticidade. A resposta certa é isolar e monitorar mais, não ignorar.
- **DLP:** Os 4 estágios de maturidade fazem sentido: primeiro entender o que você tem e onde está (não dá pra proteger o que não conhece), depois implementar tecnologia.
