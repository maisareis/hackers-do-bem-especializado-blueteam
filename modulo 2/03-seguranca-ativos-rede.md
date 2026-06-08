# Aula 3 -- Segurança de Ativos de Rede

## Conceitos-chave

-   Ativos de rede: roteadores, switches, firewalls, pontos de acesso
    Wi‑Fi, storages, sistemas VoIP
-   Classificação de ativos: crítico, sensível, operacional, público,
    regulamentado
-   Segurança em roteadores: firmware atualizado, senhas fortes,
    serviços/portas desabilitados, firewall, criptografia
-   Segurança em switches: VLANs, autenticação de portas (802.1X), ACLs,
    monitoramento de portas
-   Firewalls: tipos (pacotes, stateful, aplicação, NGFW),
    funcionalidades (controle de acesso, IDS/IPS, DMZ)
-   VLAN (Virtual Local Area Network): segmentação lógica da rede física
-   DMZ (Zona Desmilitarizada): área isolada para serviços públicos
-   Segurança Wi‑Fi: WPA2 vs WPA3, criptografia, autenticação
    (EAP/RADIUS), filtragem MAC
-   Segurança física de ativos: controle de acesso, monitoramento por
    vídeo, ambiente controlado
-   Dispositivos móveis: antivírus, patches, criptografia, gerenciamento
    remoto (wipe), conscientização

## Resumo da Aula

### Classificação de Ativos de Rede

Crítico: indispensável para operações essenciais (ex.: servidor de banco
de dados principal). Sensível: contém informações confidenciais (ex.:
dados de clientes e segredos comerciais). Operacional: essencial para o
dia a dia, mas com impacto menor (ex.: switch de acesso). Público:
acessível externamente (ex.: website). Regulamentado: sujeito a leis
específicas (ex.: dados financeiros ou de saúde).

### Segurança em Roteadores

Firmware atualizado com patches do fabricante; uso de senhas fortes;
desabilitação de serviços e portas não utilizados; configuração adequada
de firewall; utilização de criptografia, preferindo SSH em vez de Telnet
e SSL/TLS para interfaces web.

### Segurança em Switches

Uso de VLANs para segmentação lógica da rede; autenticação 802.1X para
validar dispositivos antes da liberação da porta; ACLs para controle de
tráfego; monitoramento de portas para identificar conexões não
autorizadas.

### VLAN -- Virtual Local Area Network

Permite criar redes lógicas independentes dentro da mesma infraestrutura
física, isolando departamentos, funções ou níveis de confiança. Um
exemplo comum é a separação entre rede corporativa e rede de visitantes.

### Tipos de Firewall

Firewall de pacotes inspeciona cabeçalhos (IP, porta e protocolo).
Firewall stateful mantém o estado das conexões. Firewall de aplicação
analisa conteúdo na camada 7. NGFW combina inspeção avançada, IDS/IPS,
controle de aplicações e inspeção SSL.

### DMZ (Zona Desmilitarizada)

Estrutura típica: Internet → Firewall → DMZ (Web, E-mail, DNS) →
Firewall → Rede Interna. Serviços públicos ficam isolados da rede
corporativa, reduzindo o impacto de comprometimentos.

### Segurança Wi‑Fi

WPA2 utiliza AES‑CCMP e autenticação por senha compartilhada. WPA3
utiliza SAE, autenticação mais robusta, proteção contra ataques de força
bruta offline e melhorias para redes públicas. WEP e WPA originais são
considerados inseguros.

Medidas complementares incluem autenticação EAP/RADIUS, filtragem MAC e
segmentação por VLANs.

### Segurança Física

Controle de acesso a salas de servidores, monitoramento por vídeo,
controle ambiental, racks trancados, backup off-site e descarte seguro
de equipamentos.

### Dispositivos Móveis

Uso de antivírus, aplicação de patches, criptografia de dados,
gerenciamento remoto para limpeza em caso de perda ou roubo e
treinamento de usuários.

## Meus Insights

Classificar ativos antes de protegê-los ajuda a direcionar recursos para
o que realmente importa. VLANs são importantes para segmentação, mas não
substituem firewalls entre segmentos sensíveis. Redes ainda utilizando
WEP ou WPA representam um risco significativo. Filtragem MAC pode servir
como camada adicional, mas não deve ser considerada uma proteção
confiável isoladamente. A DMZ continua sendo uma estratégia simples e
eficaz para isolamento de serviços públicos. Portas de switch não
utilizadas devem ser desabilitadas ou protegidas com 802.1X. Firewalls
stateful representam o mínimo esperado em ambientes corporativos
modernos. Por fim, a segurança física permanece essencial, pois o acesso
direto aos equipamentos pode contornar diversas camadas de proteção
lógica.
