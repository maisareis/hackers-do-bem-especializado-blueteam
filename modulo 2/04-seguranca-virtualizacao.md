# 📦 Aula 4 – Segurança em Ambientes Virtualizados

## 📌 Conceitos-chave

- Virtualização: executar múltiplos sistemas operacionais (guests/VMs) em um único servidor físico (host)
- Máquina Virtual (VM): instância virtual de um SO com recursos dedicados (CPU, memória, disco, rede)
- Hypervisor: software que cria e gerencia VMs (Tipo 1 bare-metal / Tipo 2 hosted)
- Snapshot: captura do estado de uma VM em um momento específico
- Virtual Switch: rede virtual que conecta VMs entre si e com a rede física
- Armazenamento virtualizado: abstração dos recursos de armazenamento físico
- Tipos de virtualização: servidor, desktop, rede, armazenamento, aplicativos
- Riscos: VM escape, vazamento entre VMs, vulnerabilidades no hypervisor, sprawl de VMs
- Isolamento e segmentação de rede entre VMs

## 📌 Resumo da aula

### Hypervisors: Tipo 1 (Bare-metal) vs Tipo 2 (Hosted)

| Tipo | Característica | Exemplos |
|------|----------------|----------|
| Tipo 1 (Bare-metal) | Executa diretamente no hardware, sem SO hospedeiro. Melhor desempenho. | VMware ESXi, Microsoft Hyper-V, XenServer, KVM |
| Tipo 2 (Hosted) | Executa como aplicativo em cima de um SO existente. Mais fácil de instalar. | VMware Workstation, Oracle VirtualBox, Parallels Desktop |

### Emulação vs Virtualização

| | Emulação | Virtualização |
|--|----------|---------------|
| Arquitetura | Hardware diferente do destino | Mesma arquitetura |
| Desempenho | Mais lento (traduz instruções) | Próximo do nativo |
| Caso de uso | Software legado, arquiteturas diferentes | Consolidação de servidores, nuvem |

### Riscos de Segurança na Virtualização

| Risco | Descrição |
|-------|-----------|
| VM escape | Invasor "fura" a VM e acessa o hypervisor ou outras VMs |
| Vazamento entre VMs | Acesso indevido a dados de outras VMs no mesmo host |
| Vulnerabilidades no hypervisor | Hypervisor comprometido = todas as VMs comprometidas |
| Sprawl de VMs | VMs esquecidas, sem patch, viram porta de entrada |
| Acesso privilegiado | Console de gerenciamento comprometido dá controle total |

### Práticas de Segurança para Virtualização

**Segurança do hypervisor:**
- Manter atualizado com patches de segurança
- Desabilitar serviços e recursos desnecessários
- Restringir acesso ao console de gerenciamento
- Monitorar integridade do hypervisor

**Isolamento e segmentação:**
- VLANs para separar VMs por função/departamento
- Políticas de acesso restritas entre VMs
- Limitar recursos (CPU, memória) por VM para evitar ataques de vizinhança barulhenta

**Gerenciamento de acesso privilegiado:**
- Princípio do menor privilégio aplicado aos administradores do hypervisor
- Contas administrativas individuais (nada de admin compartilhado)
- Autenticação forte (2FA) para acesso ao console
- Auditoria e monitoramento de ações privilegiadas

**Backup e recuperação:**
- Snapshots para pontos de recuperação rápidos (não substituem backup)
- Backup regular das VMs
- Testar restauração periodicamente

**Proteção contra DoS/DDoS:**
- Firewalls e IDS/IPS na infraestrutura virtualizada
- Monitoramento de recursos para detectar anomalias

## 💡 Meus Insights

**Hypervisor Tipo 1 é o padrão corporativo:** Em qualquer ambiente sério, você vai usar bare-metal. A performance e o isolamento são muito superiores. Tipo 2 é legal pro seu notebook de testes, mas não num datacenter.

**VM escape é o pesadelo do blue team:** Você protege a VM, aplica patches, configura firewall... e o invasor sai da VM e vai direto pro hypervisor. É o equivalente virtual de um invasor que sai do quarto alugado e entra na sua casa. A segurança do hypervisor tem que ser impecável.

**Sprawl de VM é real:** Já vi empresa com 300 VMs no vCenter e ninguém sabia o que 50 delas faziam. VM esquecida = patch desatualizado = risco. Ciclo de vida de VM tem que ser gerenciado igual servidor físico.

**Snapshot não é backup:** Muita gente trata snapshot como se fosse backup. Não é. Snapshot depende do disco original. Se o storage corromper, seu snapshot vai junto. Backup é cópia em outro lugar.

**Console de gerenciamento é o cofre:** Se alguém pegar seu usuário/senha do vCenter ou do Hyper-V Manager, já era. É o mesmo que ter a chave de todas as salas do prédio. Autenticação de dois fatores aí não é frescura, é necessidade.

**KVM é o rei do código aberto:** VMware ESXi é ótimo, mas paga-se. KVM (com o QEMU) é gratuito, performático e está em tudo que é nuvem (AWS, GCP, OpenStack). Saber KVM é entender como a nuvem funciona por baixo.

**Isolamento entre VMs não é automático:** Só porque estão em hypervisors diferentes não significa que estão seguras. Uma VM pode atacar a vizinha se a rede não estiver segmentada. VLANs e firewalls virtuais são obrigatórios.

**Virtualização facilitou a vida do blue team e do red team:** Antes, provisionar um servidor novo levava semanas. Agora leva minutos. Mas o red team também ganhou: clonar um ambiente para atacar, tirar snapshot antes de fazer algo destrutivo... a agilidade serve pros dois lados.