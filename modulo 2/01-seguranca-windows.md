# 🪟 Aula 1 – Segurança em Sistemas Windows

## 📌 Conceitos-chave

- WSUS (Windows Server Update Services) – gerenciamento centralizado de atualizações
- Arquiteturas WSUS: simples, com grupos, centralizada (réplicas), desconectada (offline)
- Políticas de senhas fortes: complexidade, tamanho mínimo, troca periódica, bloqueio de contas
- Princípio do Menor Privilégio – conceder apenas o necessário
- Contas de serviço – dedicadas, privilégios mínimos, senhas protegidas
- EDR (Endpoint Detection and Response) vs XDR (Extended Detection and Response)
- Backup e recuperação de dados
- Conscientização contra engenharia social e phishing

---

## 📌 Resumo da aula

### Atualizações com WSUS

O WSUS centraliza o gerenciamento de patches da Microsoft. Arquiteturas disponíveis:

| Arquitetura | Característica |
|-------------|----------------|
| Simples | Um servidor atende todos os clientes |
| Simples com grupos | Organiza clientes por departamento/função |
| Centralizada (réplicas) | Servidor principal + réplicas em filiais |
| Desconectada (offline) | Sem acesso à internet, atualização manual |

### Políticas de senhas fortes

| Requisito | Recomendação |
|-----------|---------------|
| Complexidade | Maiúscula, minúscula, número, caractere especial |
| Tamanho mínimo | 8 a 12 caracteres |
| Troca periódica | A cada 60-90 dias |
| Bloqueio de conta | Após X tentativas falhas |

**Tabela de tempo de quebra de senha (8 caracteres):**
- Só números: **instantly**
- Minúsculas: 22 minutos
- Maiúsculas + minúsculas: 1 hora
- Com números e símbolos: 8 horas

### Princípio do Menor Privilégio

- Usuário só tem acesso ao que precisa para trabalhar
- Reduz superfície de ataque
- Desafio prático: equilibrar segurança com produtividade

### Contas de serviço

- Contas dedicadas para serviços/processos
- Não vinculadas a usuários específicos
- Permitem automação e rastreabilidade

### EDR vs XDR

| | EDR | XDR |
|--|-----|-----|
| Foco | Endpoint (máquina individual) | Toda a infraestrutura (endpoint, rede, servidor, nuvem) |
| Visão | Local | Holística (a "floresta inteira") |
| Resposta | No dispositivo | Coordenada entre fontes |

### Backup

- Regular, testado, armazenado em local seguro
- Essencial para recuperação após ransomware

---

## 💡 Meus Insights

**WSUS offline:** Em redes que não podem tocar na internet (ambientes críticos como SCADA, governamentais), essa arquitetura é ouro. O trabalho manual compensa quando o risco de conexão externa é maior que o esforço operacional.

**Política de senhas:** A tabela de tempo de quebra é assustadora – 8 caracteres só com números é "instantly" pra um computador. Mas o maior problema continua sendo o humano que anota a senha no post-it colado no monitor. Tecnologia resolve só metade do problema.

**Menor privilégio na prática:** Na teoria é lindo, na prática é barraqueira. "Não consigo instalar nada" é o chamado mais comum pro TI. O desafio real é equilibrar segurança com produtividade sem virar o "chato do setor" que trava tudo.

**XDR vs EDR:** A evolução é clara. EDR olha só o endpoint – você vê que uma máquina foi comprometida. XDR olha a floresta inteira – você vê o ataque se movimentando entre máquinas, redes e nuvem. Numa rede grande, isso faz toda a diferença.

**Backup é a última linha:** Pode ter firewall, antivírus, EDR, treinamento – ransomware ainda pode passar. Backup que **funciona** é o que separa uma história chata de uma catástrofe. Testar restauração é tão importante quanto fazer a cópia.

**Conscientização não é palestra:** Enviar um slide uma vez por ano não funciona. Simulações de phishing frequentes e feedback imediato mudam comportamento de verdade. O usuário precisa sentir o erro, não só ler sobre ele.