# 📡 Aula 4 – Monitoramento e Análise de Tráfego

## 📌 Conceitos-chave

- Monitoramento de rede: captura, análise e interpretação do tráfego de dados
- Sniffer: ferramenta que captura pacotes na rede para análise
- Aquisição de tráfego: no próprio host, no segmento de rede (SPAN/TAP), no switch
- Ferramentas: tcpdump (CLI), Wireshark (GUI)
- Análise de fluxo: IP (versão), endereços de origem/destino, portas TCP/UDP, ToS
- Análise de DNS: DGA, NXDOMAIN, resolvedores seguros
- Análise de URL: partes da URL, métodos HTTP, códigos de resposta, percent encoding
- Firewall: análise de logs, conjunto de regras, filtragem de saída, firewalking
- Sinkhole e Black Hole: técnicas de redirecionamento/descarte de tráfego malicioso
- NAC (Network Access Control): controle de acesso baseado em porta (802.1X)
- Ferramentas de endpoint: AV, HIDS/HIPS, EPP, EDR, UEBA
- Análise de malware: ambiente isolado, virtualização, emulação, engenharia reversa
- Listas negras e brancas: políticas de restrição de execução (SRP, AppLocker, WDAC, LSM)
- Phishing: análise de e-mail, SPF, DKIM, DMARC, S/MIME

## 📌 Resumo da aula

### Instrumentos de Investigação em Redes

**Aquisição de tráfego:**

| Método | Descrição |
|--------|-----------|
| Próprio host | Captura diretamente no dispositivo (ex: tcpdump na máquina local) |
| SPAN (Switch Port Analyzer) | Copia tráfego de uma ou mais portas do switch para uma porta de monitoramento |
| TAP (Test Access Port) | Hardware externo que copia o tráfego sem interferência |
| Sniffer | Ferramenta que captura e analisa pacotes (tcpdump, Wireshark) |

### tcpdump – Captura de Pacotes via CLI

**Características:**
- Ferramenta leve, via linha de comando (Linux)
- Permite desabilitar resolução de nomes para melhor desempenho
- Controle de verbosidade do output
- Salvar captura em arquivos para análise posterior
- Filtros para selecionar pacotes específicos

### Wireshark – Análise Gráfica de Protocolos

**Funcionalidades:**
- Interface gráfica intuitiva
- Decodificação automática de protocolos
- Filtros personalizados (display e capture filters)
- Estatísticas de tráfego
- Gráfico de fluxo (Flow Graph)
- Análise detalhada de cada pacote (IP, portas, payload)

### Análise de Fluxo

**Elementos a analisar:**
- Versão IP (IPv4 ou IPv6)
- Endereços IP de origem e destino
- Portas TCP/UDP
- Tipo de Serviço (ToS)
- Comparação com linha de base para detectar irregularidades
- Endpoints questionáveis
- Uso de largura de banda por protocolo

### Análise de DNS

| Técnica | Descrição |
|---------|-----------|
| Listas negras de reputação | Comparar endereços IP/domínios com bases de maliciosos conhecidos |
| DGA (Domain Generation Algorithm) | Malware gera domínios dinamicamente para evitar listas negras |
| NXDOMAIN | Erro de domínio não existente – pode indicar tentativa de comunicação com C&C |
| Resolvedores seguros | DNS com filtragem de domínios maliciosos |

### Análise de URL

**Partes da URL:**
- Esquema (http://, https://)
- Nome de domínio
- Caminho do recurso
- Parâmetros de consulta
- Fragmento/âncora

**Métodos HTTP a monitorar:**
- GET (recuperar recurso)
- POST (enviar dados)
- PUT (atualizar recurso)
- HEAD (obter cabeçalhos)

**Códigos de resposta HTTP:**
- 2xx – Sucesso
- 3xx – Redirecionamento
- 4xx – Erro do cliente (404, 401)
- 5xx – Erro do servidor (500)

**Percent encoding:** Verificar se caracteres especiais foram codificados corretamente na URL.

### Análise de Logs de Firewall

**O que examinar:**
- Conexões permitidas e negadas
- Portas e protocolos utilizados
- Consumo de largura de banda
- Conversão de endereços (NAT)

**Formatos comuns de log:**
- Syslog (padrão para dispositivos de rede)
- W3C Extended (comum em servidores web)

**Conjunto de regras do firewall:**
- Listas de reputação/IPs maliciosos
- Drop vs Reject: drop ignora silenciosamente, reject envia resposta de bloqueio
- Filtragem de saída (egress): bloquear tráfego de C&C e exfiltração de dados

### Firewalking – Técnica de Mapeamento de Firewall

Envia pacotes com diferentes TTLs e analisa respostas para identificar quais portas/serviços estão bloqueados.

### Sinkhole vs Black Hole

| Técnica | Comportamento | Uso |
|---------|---------------|-----|
| Black Hole | Descarta tráfego no roteador sem notificar o destino | Eliminar tráfego malicioso/indesejado com baixo consumo de recursos |
| Sinkhole | Redireciona tráfego para ambiente controlado (honeypot/honeynet) | Analisar tráfego malicioso sem interromper tráfego legítimo |

### NAC – Network Access Control (802.1X)

**Funcionalidades:**
- Verificação de conformidade do dispositivo antes do acesso
- Medidas corretivas para dispositivos não conformes
- Controle granular de entrada na rede

### Ferramentas de Análise de Endpoint

| Ferramenta | Função |
|------------|--------|
| Antivírus (AV) | Detecção e eliminação de malware |
| HIDS/HIPS | Monitoramento de atividades suspeitas no host |
| EPP (Endpoint Protection Platform) | Solução completa (AV, firewall, IDS) |
| EDR (Endpoint Detection and Response) | Registro de eventos, investigação, restauração de estado |
| UEBA | Análise de comportamento de usuários e entidades (machine learning) |

### Análise de Malware em Ambiente Isolado

**Práticas recomendadas:**
- Executar em ambiente controlado (sandbox, VM) – nunca em produção
- Usar virtualização para impedir propagação
- Emular recursos externos (DNS, servidores) para observar comportamento
- Engenharia reversa (desmontagem, descompilação, análise de strings)
- Identificar empacotadores (packers) que ofuscam o código

### Análise de Comportamento com Process Explorer

- **Process Explorer:** Ver hierarquia de processos, recursos, atividades suspeitas
- **Process Monitor:** Monitorar registro, sistema de arquivos, rede
- **AutoRuns:** Controlar programas executados automaticamente no boot

### Listas Negras e Brancas

| Tipo | Política | Uso |
|------|----------|-----|
| Lista Negra | Negar acesso a itens da lista | Bloquear recursos maliciosos conhecidos |
| Lista Branca | Permitir apenas itens da lista | Controle rigoroso, só executa autorizados |

**Ferramentas de restrição de execução:**
- SRP (Software Restriction Policies)
- AppLocker
- WDAC (Windows Defender Application Control)
- LSM (Linux Security Module)

### Phishing por E-mail

**Técnicas comuns:**
- Pretexting: histórias fictícias para enganar a vítima
- Representação (spoofing): se passar por entidade confiável
- Redirecionamento/encaminhamento para URLs maliciosas

**Análise de cabeçalho de e-mail:**
- From (Mostrar de)
- Envelope from (endereço de resposta em caso de rejeição)
- Received from/by (caminho dos MTAs)
- SPF, DKIM, DMARC

**Proteção do servidor de e-mail:**
- **SPF (Sender Policy Framework):** Lista de IPs autorizados a enviar pelo domínio
- **DKIM (DomainKeys Identified Mail):** Assinatura digital no cabeçalho
- **DMARC (Domain-based Message Authentication):** Política para quando SPF/DKIM falham
- **Domínios primos:** Domínios com nome semelhante ao original (ex: "rnicrosoft.com")
- **S/MIME:** Criptografia e assinaturas digitais em e-mails

### Indicadores de Comprometimento (IOCs) em Phishing

- Anexos suspeitos (malware embutido)
- URLs embutidas (redirecionamento para sites falsos)
- Erros de português/ortografia
- Urgência falsa ("sua conta será bloqueada")
- Remetente desconhecido ou com domínio parecido

## 💡 Meus Insights

**Sniffer não é invasão, é diagnóstico:** Ter um sniffer na rede (promiscuous mode) é essencial para o blue team. Você só consegue resolver o que consegue enxergar. Wireshark num SPAN de switch resolve 80% dos problemas de troubleshooting e detecção.

**SPAN vs TAP:** SPAN é prático (já está no switch), mas pode dropar pacotes sob alta carga. TAP é hardware dedicado, mais caro, mas não perde pacote. Em redes críticas (financeiro, saúde), TAP é investimento necessário.

**tcpdump no servidor Linux é vida:** Servidor com problema de rede, sem acesso à GUI? `tcpdump -i eth0 -s 1500 -w captura.pcap` resolve. Depois abre o arquivo no Wireshark no seu desktop. É o workflow padrão de qualquer sysadmin decente.

**DGA é fascinante e assustador:** Malware que gera domínios dinamicamente (Conficker, Kraken) torna o bloqueio por lista negra quase inútil. O blue team precisa de análise estatística e machine learning pra detectar padrões nos domínios gerados.

**Firewalking mostra o que o firewall esconde:** Técnica antiga, mas ainda útil. Você mapeia as regras de filtragem sem nunca ter acesso ao dispositivo. Testar seus próprios firewalls com firewalking é um bom exercício de autoconhecimento.

**Sinkhole é inteligência de ameaça pura:** Redirecionar tráfego de malware pra sua própria infraestrutura controlada (honeypot) te permite estudar o ataque em tempo real. Empresas grandes mantêm sinkholes próprios para entender campanhas direcionadas.

**EDR é o novo padrão de endpoint:** Antivírus já foi suficiente, mas hoje o EDR (com detecção comportamental) é o mínimo. AV olha assinatura, EDR olha comportamento. E com resposta (containment, rollback), fica muito mais poderoso.

**Lista branca é o sonho do segurança:** Executar só o que está explicitamente autorizado é a forma mais segura de operar. Mas o custo operacional é alto – cada novo aplicativo precisa ser aprovado e adicionado. Em ambientes controlados (kiosk, terminal bancário), é viável e recomendado.

**Phishing ainda é o vetor #1:** Mais de 90% dos ataques começam com um e-mail de phishing. Usuário continua sendo o elo mais fraco. SPF, DKIM e DMARC são ferramentas poderosas, mas nada substitui a conscientização e treinamento frequente (com simulações).

**SPF, DKIM e DMARC funcionam juntos:** SPF diz "esses IPs podem enviar por mim". DKIM diz "esse e-mail não foi adulterado". DMARC diz "o que fazer se as verificações falharem". Implementar os três reduz drasticamente spoofing do seu domínio.