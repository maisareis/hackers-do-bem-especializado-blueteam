# Aula 5 -- Gerenciamento de Logs Centralizados

## Conceitos-chave

-   Logs: registros de eventos em sistemas e redes
-   Gerenciamento centralizado de logs: coleta, armazenamento, análise e
    correlação
-   SIEM (Security Information and Event Management)
-   Arquitetura de logs: coleta, armazenamento, análise e visualização
-   Syslog e RFC 3195
-   Formatos e classificação de logs
-   Gravidade (severity) de 0 a 7
-   Ferramentas SIEM: ELK, Splunk, QRadar, ArcSight, Graylog, OSSIM
-   Correlação de eventos e análise comportamental
-   Dashboards, KPIs e compliance

## Resumo da Aula

### O que são Logs e Por que São Importantes

Logs são registros de eventos utilizados para troubleshooting,
auditoria, detecção de ameaças, otimização de desempenho e investigações
forenses. No contexto de Blue Team, permitem detectar acessos indevidos,
monitorar tráfego, responder a incidentes e reconstruir ataques.

### Diretrizes para Criação de Logs

Definir quais dispositivos geram logs, quais eventos devem ser
registrados, quais informações serão armazenadas (usuário, IP, timestamp
e ação) e a frequência de geração.

### Transferência de Logs

Determinar quais hosts enviam logs para a infraestrutura central, quais
protocolos serão utilizados, a frequência de envio e os mecanismos de
proteção da confidencialidade, integridade e disponibilidade.

### Armazenamento e Remoção

Definir rotação, retenção, preservação para requisitos legais, espaço
necessário e procedimentos de remoção segura.

### Análise de Logs

Determinar frequência de análise, responsáveis pelo acesso, ações diante
de atividades suspeitas e proteção dos resultados obtidos.

### Syslog

Formato composto por PRI, Header e Mensagem. O PRI contém Facility e
Severity. O Header inclui timestamp e hostname. A mensagem contém
identificação da aplicação e detalhes do evento.

Severity: 0 Emergency, 1 Alert, 2 Critical, 3 Error, 4 Warning, 5
Notice, 6 Informational, 7 Debug.

### RFC 3195

Utiliza TCP (porta 1468), TLS para criptografia e MD5 para validação de
integridade.

### SIEM

Integra logs de múltiplas fontes, correlaciona eventos, detecta ameaças
e auxilia na resposta a incidentes. Sua arquitetura inclui agentes,
sensores, coleta, armazenamento centralizado, mecanismo de correlação e
dashboards.

### Soluções SIEM

ELK/Elastic Stack, Splunk, QRadar, ArcSight, Graylog e AlienVault/OSSIM.

### Padronização de Logs

Os principais desafios incluem formatos diferentes, horários
inconsistentes e grandes volumes de dados. As soluções incluem NTP,
normalização de logs, criptografia e políticas de retenção.

### Correlação de Eventos

Pode utilizar assinaturas, heurística, machine learning, análise
comportamental, análise de anomalias e padrões temporais.

Exemplo: Error.LoginFailure \> 3 AND LoginFailure.User AND Duration \< 1
hour

### Dashboards e KPIs

MTTD, MTTR, taxa de detecção de ameaças, falsos positivos, tempo médio
de resolução, cobertura de eventos, conformidade e resolução de
vulnerabilidades.

### Compliance e Retenção

LGPD, GDPR, PCI DSS, SOX, HIPAA, FISMA, GLBA e Marco Civil da Internet
possuem requisitos específicos relacionados à retenção e tratamento de
logs.

### Atividades Diárias com SIEM

Triagem de alertas, revisão de fontes de segurança, análise de
inteligência de ameaças, execução de varreduras e hunting de ameaças.

## Meus Insights

Log não serve apenas para investigar falhas; ele permite monitoramento
proativo e identificação antecipada de problemas. SIEM exige manutenção
constante e ajuste fino das regras para evitar excesso de falsos
positivos e falsos negativos. ELK Stack é uma das plataformas open
source mais populares para gerenciamento e análise de logs. Syslog
continua sendo uma habilidade fundamental para profissionais de
infraestrutura e segurança. Timestamps sincronizados por NTP são
indispensáveis para investigações forenses. Falsos positivos reduzem a
confiança no sistema de monitoramento e devem ser minimizados. A
retenção de logs exige equilíbrio entre requisitos legais, custos e
necessidades operacionais. Threat Hunting depende fortemente da
qualidade dos logs e da capacidade de consulta do SIEM. Dashboards devem
ser adaptados ao público-alvo, atendendo tanto necessidades técnicas
quanto gerenciais.
