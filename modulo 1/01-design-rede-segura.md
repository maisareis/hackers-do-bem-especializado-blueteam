# Aula 1 – Design de Rede Segura

## 📌 Segmentação de Rede
Dividir a rede em partes menores para limitar o impacto de um ataque e dificultar a movimentação lateral do invasor.

**Por que segmentar:**
- Reduz a superfície de ataque
- Permite controle de acesso granular por segmento
- Isola um comprometimento antes que ele se espalhe

**Como fazer:**
- Identificar os segmentos necessários: servidores críticos, usuários, IoT, convidados
- Criar políticas de acesso restritivas para cada um
- Usar firewalls e ACLs para controlar o tráfego entre segmentos
- Implementar IDS/IPS para detectar comportamentos anômalos
- Manter patches em dia e realizar testes de penetração periódicos

---

## 📌 Topologia e Zonas de Rede
A topologia define como os dispositivos se conectam. Zonas aplicam diferentes níveis de confiança.

**DMZ (Zona Desmilitarizada):**
Área separada onde ficam os serviços públicos (servidor web, e-mail, DNS). Fica entre o firewall de perímetro e o firewall interno, então um atacante que comprometer a DMZ ainda não chegou na rede interna.

---

## 📌 Comutação e Roteamento Seguros

**Ataques comuns na Camada 2:**
- **ARP Poisoning** → envia pacotes ARP falsos para associar o MAC do atacante a um IP legítimo e interceptar o tráfego
- **MAC Flooding** → sobrecarrega a tabela CAM do switch, que passa a funcionar como hub (encaminha pra todo mundo)
- **MITM (Man-in-the-Middle)** → o atacante se posiciona entre dois dispositivos e intercepta/modifica a comunicação

**STP (Spanning Tree Protocol):**
Protocolo que evita loops em redes de Camada 2 bloqueando links redundantes. Problemas: convergência lenta após mudanças na topologia, subutilização dos links bloqueados e vulnerabilidade a ataques com pacotes BPDU maliciosos.

**Outras medidas:**
- Port security e filtro de MAC para controlar quem pode usar cada porta
- NAC (Network Access Control) para autenticar dispositivos antes de entrar na rede
- Autenticação nos protocolos de roteamento para evitar spoofing de rotas

---

## 📌 Balanceadores de Carga
Distribuem o tráfego entre vários servidores para evitar sobrecarga.

**Algoritmos comuns:** Round Robin, Least Connection, Hashing

**Benefícios:**
- Alta disponibilidade: se um servidor cair, o tráfego vai para outro
- Escalabilidade horizontal: adicionar servidores sem interrupção
- Ajuda na mitigação de DDoS quando combinado com IDS/IPS

**Clustering:** agrupa servidores numa entidade lógica única para redundância e eliminação de pontos únicos de falha.

**QoS (Quality of Service):** prioriza tipos de tráfego quando os recursos são disputados.

---

## 📌 Dispositivos de Segurança de Rede

| Dispositivo | O que faz |
|-------------|-----------|
| **Firewall de pacotes** | Analisa cabeçalho (IP, porta, protocolo) e decide se deixa passar |
| **Firewall Stateful** | Analisa o estado da conexão, não só o cabeçalho – muito mais seguro |
| **Proxy / Gateway** | Filtra conteúdo, autentica usuários e faz cache |
| **NAT** | Traduz endereços IP internos para um IP público, escondendo a estrutura interna |
| **Firewall Virtual** | Roda em VM ou container; flexível para ambientes cloud |

**ACLs:** conjuntos de regras que definem o que é permitido ou negado com base em IP, porta e protocolo.

**Open source vs. proprietário:**
- Open source: transparência, customização, sem custo de licença, comunidade ativa
- Proprietário: recursos exclusivos, suporte técnico dedicado, pode envolver custos

---

## 📌 IPv6
- Resolve o problema de escassez de endereços do IPv4 (~3,4 × 10³⁸ endereços)
- Formato: oito grupos de quatro dígitos hexadecimais separados por `:`
- Suporte nativo a IPSec, criptografia e QoS
- Desafio: coexistência com IPv4, compatibilidade com legado, necessidade de reconfigurar toda a infraestrutura

---

## 💡 Meus Insights
- **DMZ:** A lógica da DMZ é simples mas poderosa: expor o mínimo possível na internet. Tudo que pode ser acessado de fora fica num compartimento separado, com o castelo (rede interna) protegido atrás.
- **MITM:** Percebi que o ARP Poisoning é a base de muitos ataques mais complexos. Se você controla o ARP, você controla quem fala com quem na rede local.
- **STP:** Interessante que um protocolo criado para proteger a rede (evitar loops) também pode ser usado como vetor de ataque. Tudo que processa pacotes pode ser abusado.
- **Balanceador de carga:** Além de performance, ele é um elemento de resiliência – e isso tem muito a ver com Disponibilidade da tríade CIA.
- **Firewall Stateful:** A diferença pro stateless é enorme na prática. Um firewall de pacotes não sabe se aquele pacote faz parte de uma conexão legítima ou não. O stateful sabe.
