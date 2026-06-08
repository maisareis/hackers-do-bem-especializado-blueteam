# 🛡️ Aula 1 – Gerenciando e Monitorando Vulnerabilidades

## 📌 Conceitos-chave

- Ferramentas de enumeração: Nmap, Zenmap, hping, Responder, Aircrack-ng, Reaver, Hashcat
- OSINT (Open Source Intelligence) – coleta de informações de fontes públicas
- Fingerprinting – identificação de SO, versões, serviços, CPE
- Estados de porta no Nmap: Open, Closed, Filtered, Unfiltered, Open/Filtered, Closed/Filtered
- Técnicas de varredura: TCP ACK, varredura ociosa (-sI), fragmentação (-f), scan-delay
- Critérios de varredura: segmentação, IDS/IPS, firewall, cronograma, restrições
- Níveis de varredura: descoberta, rápida, completa, conformidade
- Padrões de identificação: CVE, CWE, CAPEC, CPE, CCE
- CVSS (Common Vulnerability Scoring System) – pontuação base, ambiental, temporal
- Falsos positivos e falsos negativos na avaliação de vulnerabilidades

## 📌 Resumo da aula

### Ferramentas de Enumeração e Varredura

| Ferramenta | Função |
|------------|--------|
| Nmap/Zenmap | Varredura de portas, fingerprinting, detecção de SO e serviços |
| hping | Criação e injeção de pacotes personalizados, rastreamento de rota, carimbo de data/hora |
| Responder | Manipulação de resolução de nomes (LLMNR, NBT-NS) |
| Aircrack-ng | Análise de redes Wi-Fi, captura de quadros, quebra de chaves |
| Reaver | Exploração de WPS em roteadores |
| Hashcat | Quebra de senhas (dicionário, força bruta, máscaras) com aceleração GPU |

### Estados de Porta no Nmap

| Estado | Significado |
|--------|-------------|
| Open | Porta com aplicativo recebendo conexões |
| Closed | Porta responde mas não tem aplicativo ouvindo |
| Filtered | Firewall ou filtro bloqueando a sondagem |
| Unfiltered | Porta testada mas não foi possível determinar se está aberta/fechada |
| Open/Filtered | Não foi possível distinguir entre aberta e filtrada |
| Closed/Filtered | Não foi possível distinguir entre fechada e filtrada |

### Técnicas de Varredura com Nmap

- `-sn` – suprimir varredura de portas (apenas identificar hosts ativos)
- `-sL` – listagem de hosts sem enviar pacotes
- `-PS` – ping TCP SYN
- `-sI <zumbi> <alvo>` – varredura ociosa (usando host intermediário)
- `-f` ou `--mtu` – fragmentação de pacotes
- `--scan-delay` – atraso entre pacotes para evitar detecção

### Fingerprinting com Nmap

Informações identificadas:
- Sistema operacional e versão
- Versão do aplicativo/serviço
- Nome do servidor
- Categoria e modelo do dispositivo
- CPE (Common Platform Enumeration)

### Resolução de Nomes em Redes Windows (LLMNR/NBT-NS)

- Tecnologias usadas para resolver nomes localmente quando o DNS falha
- Vulneráveis a ataques de spoofing (Responder envia respostas falsas)
- Mitigação: desativar LLMNR e NBT-NS ou direcionar forçadamente o destino

### Critérios para Varreduras de Vulnerabilidade

**Fatores a considerar:**
- Segmentação de rede (VLANs, sub-redes)
- Configurações de IDS/IPS e firewall (evitar falsos positivos e bloqueios)
- Disponibilidade de largura de banda
- Utilização de recursos (CPU, memória, disco)
- Sensibilidade dos dados
- Requisitos regulatórios (LGPD, GDPR, PCI DSS)

**Níveis de sensibilidade da varredura:**

| Nível | Descrição |
|-------|-----------|
| Descoberta | Enumeração de serviços e detecção de hosts (sem testes específicos) |
| Rápida | Plug-ins específicos para o alvo, evita plug-ins arriscados |
| Completa | Todos os plug-ins, incluindo os arriscados, varredura aprofundada |
| Conformidade | Configurada para atender a modelo regulatório específico |

### Potenciais Riscos da Varredura

- Impacto no desempenho de rede e sistemas
- Risco de indisponibilidade do sistema (sobrecarga)
- Exposição de informações sensíveis nos resultados
- Uso indevido de credenciais de varredura
- Expansão da superfície de ataque (portas abertas para ferramentas)

### Padrões de Identificação de Vulnerabilidades

| Padrão | Significado |
|--------|-------------|
| CVE | Vulnerabilidades e Exposições Comuns (identificador único) |
| CWE | Enumeração de Fraquezas Comuns |
| CAPEC | Enumeração e Classificação de Padrões de Ataque Comuns |
| CPE | Enumeração de Plataforma Comum |
| CCE | Enumeração de Configuração Comum |

### CVSS – Sistema de Classificação de Vulnerabilidades Comuns

**Componentes da pontuação:**
- **Pontuação Base** – atributos intrínsecos da vulnerabilidade
- **Componente Ambiental** – características específicas do ambiente
- **Componente Temporal** – evolução da vulnerabilidade ao longo do tempo

**Métricas fundamentais:**
- Vetor de Acesso (VA)
- Complexidade de Acesso (CA)
- Privilégios Necessários (PN)
- Interface do Usuário (IU)
- Escopo (ES)
- Confidencialidade (C), Integridade (I), Disponibilidade (A)

### Classificação dos Resultados da Varredura

| Classificação | Significado |
|---------------|-------------|
| Verdadeiro Positivo | Vulnerabilidade legítima que representa risco real |
| Falso Positivo | Ferramenta indicou vulnerabilidade que não existe |
| Verdadeiro Negativo | Ferramenta não detectou onde realmente não havia |
| Falso Negativo | Ferramenta não identificou uma vulnerabilidade real |

## 💡 Meus Insights

**Nmap é o canivete suíço do blue team:** Saber usar Nmap direito separa o profissional comum do cara que realmente entende de rede. Não é só rodar `nmap -sV -p-`. Entender os estados das portas, saber quando usar fragmentação ou scan-delay, e interpretar o fingerprinting corretamente faz toda diferença numa investigação real.

**Varredura ociosa é arte:** A técnica `-sI` é linda. Você usa um "zumbi" (host intermediário) para escanear o alvo sem seu IP real aparecer. Além de furtividade, mostra como o TCP/IP pode ser manipulado. É um ótimo exemplo de como conhecimento profundo de protocolo vira vantagem tática.

**OSINT é subestimado pelo blue team:** Muita gente pensa em OSINT só pra ataque, mas o blue team deveria usar mais. Pesquisar seu próprio domínio, ver o que vaza em Github, Pastebin, fóruns, é segurança ofensiva aplicada à defesa. Você descobre o que o invasor vai encontrar antes dele.

**Falso negativo é mais perigoso que falso positivo:** Falso positivo incomoda, gasta tempo. Falso negativo te dá falsa sensação de segurança. É pior. Por isso varreduras com diferentes ferramentas e métodos é importante. Uma ferramenta sozinha nunca é suficiente.

**CVSS não é verdade absoluta:** Uma vulnerabilidade com CVSS 10 pode ser irrelevante se o ativo não é crítico ou não está exposto. E uma com CVSS 5 pode ser um desastre num servidor de borda com dados sensíveis. O escore ajuda, mas contexto é rei. Ajustar o componente ambiental é obrigatório, não opcional.

**Hashcat é um monstro:** Com GPU, ele quebra senhas em velocidades assustadoras. A tabela de tempo de quebra do Módulo 2 fica pequena perto do que um cluster de GPUs faz. Isso mostra que senha sozinha já era. 2FA ou MFA não é luxo, é necessidade.

**WPS é uma porta dos fundos:** O Reaver existe porque o WPS (Wi-Fi Protected Setup) é inerentemente inseguro. Desativar WPS em roteadores deveria ser regra número 1 de segurança Wi-Fi, mas muitos vêm com ele ligado por padrão. É a primeira coisa que desativo num AP novo.