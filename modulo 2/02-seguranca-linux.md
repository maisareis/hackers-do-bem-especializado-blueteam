# 🐧 Aula 2 – Segurança em Sistemas GNU/Linux

## 📌 Conceitos-chave

- OpenLDAP e autenticação centralizada de usuários
- LDAP (Lightweight Directory Access Protocol) – versões v2, v3 e v3.1
- Gerenciamento de configuração com Ansible (agentless, YAML, push-based)
- Comparação: Ansible vs Puppet vs Chef
- Gerenciamento de logs: syslog, logrotate, servidor centralizado
- Serviços essenciais GNU/Linux: Apache, OpenSSH, Samba, BIND, MariaDB/MySQL, OpenVPN, QEMU/KVM
- Princípios da segurança: Confidencialidade, Integridade, Disponibilidade, Autenticidade, Não-repúdio

---

## 📌 Resumo da aula

### Autenticação Centralizada com OpenLDAP

O OpenLDAP é um serviço de diretório que centraliza contas de usuários em ambiente Linux.

**O que é um serviço de diretório?**
- Armazena informações de forma hierárquica (árvore)
- Usado para autenticação, autorização, gerenciamento de identidade
- Estrutura chamada DIT (Directory Information Tree)

**LDAP – protocolo de acesso a diretórios**

| Versão | Principais características |
|--------|---------------------------|
| LDAPv2 | Primeira versão, não suportava autenticação forte nem criptografia |
| LDAPv3 | Autenticação forte (SASL), TLS/SSL, controles estendidos, Unicode |
| LDAPv3.1 | Referências entre diretórios, operações assíncronas |

### Gerenciamento de Configuração com Ansible

Ansible é uma ferramenta agentless (não precisa instalar nada nos clientes) que usa SSH para executar tarefas.

**Características:**
- Playbooks em YAML (fácil de ler/escrever)
- Arquitetura push-based (você empurra as configurações)
- Desenvolvido pela RedHat

**Comparação com outras ferramentas:**

| Ferramenta | Linguagem | Agente | Curva de aprendizado |
|------------|-----------|--------|---------------------|
| Ansible | YAML | Agentless | Baixa |
| Puppet | Puppet DSL | Requer agente | Média/Alta |
| Chef | Ruby | Requer agente | Alta |

### Gerenciamento de Logs

**Localização padrão:** `/var/log/`

**Principais arquivos:**
- `/var/log/syslog` – mensagens do sistema
- `/var/log/auth.log` – eventos de autenticação

**Ferramentas:**
- `syslog` – sistema padrão
- `logrotate` – rotação e compressão de logs
- `rsyslog` – versão avançada com filtros e envio remoto

### Serviços Essenciais no GNU/Linux

| Serviço | Função |
|---------|--------|
| Apache | Servidor web |
| OpenSSH | Acesso remoto seguro, transferência de arquivos, tunelamento |
| Samba | Integração com redes Windows (compartilhamento de arquivos/impressoras) |
| BIND | Servidor DNS |
| MariaDB/MySQL | Banco de dados relacional |
| OpenVPN | VPN segura |
| QEMU/KVM | Virtualização (KVM é Type 1, QEMU é emulação) |

**Virtualização no Linux:** QEMU com aceleração KVM – desempenho próximo ao nativo

---

## 💡 Meus Insights

**LDAP é poderoso mas não é mágico:** Centralizar autenticação facilita a vida, mas cria um ponto crítico. Se o servidor LDAP cair, ninguém entra. Se for comprometido, o invasor tem a chave do castelo. Colocar réplicas e monitoramento não é luxo, é necessidade.

**Ansible vs concorrência:** A beleza do Ansible é não precisar de agente. Em um ambiente com 500 servidores, instalar e manter agente do Puppet ou Chef é um trabalho por si só. Ansible chega via SSH, faz o serviço e vai embora. Simplicidade é segurança.

**Agentless tem preço:** Por não ter agente, cada execução do Ansible precisa se conectar via SSH. Em escala muito grande (milhares de servidores), isso pode ficar lento. Mas pra 95% dos casos, vale o trade-off.

**Logs são ouro forense:** O invasor apaga logs locais. Por isso servidor centralizado de logs não é opção, é requisito. Num incidente, seus logs centralizados podem ser a única evidência de que algo aconteceu.

**OpenSSH é um canivete suíço:** Todo mundo usa SSH pra acesso remoto, mas poucos exploram túneis e proxy. Dá pra acessar um banco de dados que não tem IP público através de um túnel SSH. É uma camada extra de segurança simples e eficaz.

**KVM é o queridinho dos datacenters:** VMware ESXi é pago e robusto, mas KVM é gratuito e está em tudo que é nuvem (AWS, GCP, OpenStack). Saber KVM é saber como a nuvem funciona por baixo dos panos.

**Samba ainda vive:** Mesmo com todo mundo migrando pro cloud, o Samba continua sendo a ponte entre mundos Windows e Linux em empresas híbridas. Saber configurar um domínio Samba é skill valiosa.

**Logrotate é herói silencioso:** Já vi servidor parar porque o `/var/log` encheu. Ninguém lembra do logrotate até ele salvar seu final de semana. Configure rotação, compressão e retenção desde o dia 1.