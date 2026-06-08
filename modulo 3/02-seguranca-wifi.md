# 📶 Aula 2 – Segurança em Redes Wi-Fi

## 📌 Conceitos-chave

- Redes sem fio: WLAN, WPAN, WMAN, WWAN
- Padrões IEEE 802.11: a/b/g/n/ac/ax (Wi-Fi 4, 5, 6)
- Frequências: 2,4 GHz (maior alcance) e 5 GHz (maior velocidade)
- SSID (Service Set Identifier) – nome da rede
- Modos de operação: Infraestrutura (com AP), Ad hoc (P2P), Mesh
- Protocolos de segurança: WEP, WPA, WPA2 (Personal/Enterprise), WPA3 (Personal/Enterprise)
- Criptografia: RC4 (WEP/WPA), TKIP (WPA), AES (WPA2/WPA3), SAE (WPA3)
- Autenticação: PSK (chave pré-compartilhada), EAP/RADIUS (Enterprise)
- Ameaças: Sniffing, Spoofing, MITM, DoS/DDoS, Força Bruta, Roubo de dispositivos, Acesso à interface web do AP
- Ferramentas: Aircrack-ng, Reaver, Hashcat

## 📌 Resumo da aula

### Tipos de Redes Sem Fio

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| WPAN | Área pessoal (curta distância) | Bluetooth, Zigbee |
| WLAN | Rede local sem fio | Wi-Fi doméstico/empresarial |
| WMAN | Rede metropolitana | WiMAX |
| WWAN | Rede de longa distância | 3G/4G/5G |

### Modos de Operação

- **Infraestrutura:** Dispositivos se conectam a um ponto de acesso (AP) central. Padrão em empresas e residências.
- **Ad hoc:** Dispositivos se comunicam diretamente, sem AP. Útil para redes temporárias, mas menos segura.
- **Mesh:** Vários nós se interconectam, criando uma teia redundante. Auto-organizável e resiliente.

### Padrões 802.11 (Wi-Fi)

| Padrão | Frequência | Velocidade Máx. | Alcance | Segurança | Ano |
|--------|------------|----------------|---------|-----------|-----|
| 802.11b | 2,4 GHz | 11 Mbps | 140 m | WEP, WPA, WPA2 | 1999 |
| 802.11a | 5 GHz | 54 Mbps | 120 m | WEP, WPA, WPA2 | 1999 |
| 802.11g | 2,4 GHz | 54 Mbps | 140 m | WEP, WPA, WPA2 | 2003 |
| 802.11n | 2,4/5 GHz | 600 Mbps | 250 m | WPA2 | 2009 |
| 802.11ac | 5 GHz | 1,3 Gbps | 120 m | WPA2 | 2013 |
| 802.11ax | 2,4/5 GHz | 9,6 Gbps | 120 m | WPA3 | 2019 |

**Wi-Fi 6 (802.11ax)** – Tecnologias: OFDMA, MU-MIMO aprimorado, maior eficiência em ambientes densos.

### Protocolos de Segurança Wi-Fi

| Protocolo | Criptografia | Autenticação | Status |
|-----------|--------------|--------------|--------|
| WEP | RC4 (chave estática) | PSK | ❌ Inseguro, descontinuado |
| WPA | TKIP (RC4 dinâmico) | PSK ou EAP | ⚠️ Obsoleto, vulnerável |
| WPA2 | AES-CCMP | PSK (Personal) ou EAP (Enterprise) | ✅ Seguro, padrão atual |
| WPA3 | AES-GCMP, SAE | SAE (Personal) ou EAP (Enterprise) | ✅ Mais seguro, emergente |

### WPA2 vs WPA3

| Característica | WPA2 | WPA3 |
|----------------|------|------|
| Criptografia | AES-CCMP | AES-GCMP (192 bits opcional) |
| Autenticação (Personal) | PSK (senha compartilhada) | SAE (Simultaneous Authentication of Equals) |
| Proteção contra força bruta | Limitada | Proteção offline robusta |
| Redes públicas | Sem proteção (texto claro) | Enhanced Open (criptografia individual) |
| Autenticação Individual | Não | Sim (cada dispositivo tem chave única) |

### WPA2-Enterprise

**Componentes:**
- Servidor de autenticação (RADIUS)
- Certificados digitais (EAP-TLS, PEAP, EAP-TTLS)
- Métodos EAP para autenticação flexível

**Diferencial:** Autenticação individual por usuário/dispositivo, não apenas pela senha da rede.

### Principais Ameaças a Redes Wi-Fi

| Ameaça | Descrição | Mitigação |
|--------|-----------|------------|
| Sniffing | Monitoramento passivo do tráfego | Criptografia WPA2/WPA3, VPN |
| Spoofing | Falsificação de AP ou dispositivo legítimo | Autenticação forte (EAP), certificados |
| MITM | Interceptação entre cliente e AP | Criptografia ponta a ponta, VPN |
| DoS/DDoS | Sobrecarga da rede/AP | Firewalls, IDS/IPS, monitoramento |
| Força bruta | Tentativa de adivinhar senha | Senha forte, WPA3, bloqueio de tentativas |
| Acesso à interface web do AP | Alteração de configurações por invasor | Firmware atualizado, senha forte, restrição de acesso, desabilitar acesso WAN |

### Ferramentas de Ataque a Wi-Fi (para conhecimento defensivo)

| Ferramenta | Função |
|------------|--------|
| Aircrack-ng | Modo monitoramento, captura de quadros, injeção de pacotes, quebra de chaves WEP/WPA |
| Reaver | Exploração de vulnerabilidades no WPS |
| Hashcat | Quebra de hashes de senha (dicionário, força bruta, máscaras) com GPU |

### Medidas de Proteção

- Utilizar **WPA2 ou WPA3** (nunca WEP ou WPA original)
- Senha forte (mínimo 12 caracteres, complexa)
- Ocultar SSID (camada extra, mas não segurança absoluta)
- Autenticação EAP/RADIUS (empresas)
- Segmentação com VLANs (redes de convidados isoladas)
- Filtragem MAC (útil como camada extra, mas não infalível)
- Manter firmware do AP atualizado
- Desabilitar acesso à interface web pela WAN
- Restringir acesso à interface web por IP
- Desabilitar WPS
- Monitoramento contínuo com IDS/IPS

## 💡 Meus Insights

**WEP é coisa do passado, mas ainda existe:** Inacreditável, mas ainda vejo redes WEP em produção em 2024. Principalmente em equipamentos antigos de pequenas empresas. Quebrar WEP leva menos de 5 minutos com Aircrack-ng. Se você achar um WEP, considere isso um chamado aberto.

**WPA2-PSK é seguro, mas com ressalvas:** A senha da rede é compartilhada entre todos. Se um funcionário sai, você tem que trocar a senha em TODO dispositivo. Em empresas médias/grandes, isso é inviável. WPA2-Enterprise com RADIUS resolve isso, mas exige mais infraestrutura.

**WPA3 é o futuro, mas a adoção é lenta:** O SAE (Simultaneous Authentication of Equals) resolve o problema do ataque offline de força bruta que existe no WPA2. Mas muitos dispositivos antigos não suportam WPA3. O período de transição será longo.

**Redes abertas são um perigo público:** Em qualquer rede Wi-Fi aberta (shopping, aeroporto, café), assume-se que alguém está sniffando. Dados em texto claro (HTTP, FTP, Telnet) são imediatamente comprometidos. VPN ou navegação exclusivamente HTTPS minimizam o risco.

**Ocultar SSID não esconde a rede:** Ferramentas de wardriving encontram redes com SSID oculto facilmente. Ocultar SSID pode atrapalhar usuários legítimos mais que invasores. Não confie nisso como medida de segurança.

**WPS é uma falha de design:** O WPS foi criado para facilitar a conexão (botão físico ou PIN de 8 dígitos). O PIN de 8 dígitos é vulnerável a brute force (o último dígito é checksum, então na prática são 10⁷ combinações, testáveis em horas). Desative WPS em qualquer AP novo imediatamente.

**Wi-Fi 6 trouxe melhorias de segurança nativas:** O WPA3 é obrigatório para certificação Wi-Fi 6, o que força o mercado a adotar criptografia mais forte e autenticação mais robusta. A longo prazo, isso vai elevar o padrão mínimo de segurança.

**AP doméstico em empresa é risco:** Muitas empresas pequenas usam roteadores de consumo (TP-Link, D-Link domésticos) em vez de APs empresariais (UniFi, Aruba, Cisco). Além de performance, a falta de firmware atualizado e de recursos de segurança (RADIUS, VLAN, monitoramento) é um risco enorme.