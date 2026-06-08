# 🛠️ Comandos Úteis – BlueTeam

Referência rápida de comandos para redes, Linux, Windows e ferramentas de segurança.

---

## 📡 Rede e Monitoramento

### Nmap – Varredura de portas e fingerprinting

| Comando | Descrição |
|---------|-----------|
| `nmap -sV <alvo>` | Detecta versões dos serviços nas portas abertas |
| `nmap -sS <alvo>` | Varredura SYN stealth (meio aberto) |
| `nmap -sU <alvo>` | Varredura UDP |
| `nmap -p- <alvo>` | Varre todas as portas (1-65535) |
| `nmap -sV -O <alvo>` | Detecta versões e sistema operacional |
| `nmap -A <alvo>` | Modo agressivo: SO, versões, scripts, traceroute |
| `nmap -sn <rede>` | Descobre hosts ativos (ping scan, sem varredura de portas) |
| `nmap -sL <rede>` | Lista hosts sem enviar pacotes |
| `nmap -PS <alvo>` | Ping TCP SYN |
| `nmap -sI <zumbi> <alvo>` | Varredura ociosa (usando host intermediário) |
| `nmap -f <alvo>` | Fragmenta pacotes para evadir firewalls |
| `nmap --scan-delay <tempo> <alvo>` | Atraso entre pacotes (evita detecção) |
| `nmap -oN arquivo.txt <alvo>` | Salva resultado em formato normal |
| `nmap -oG arquivo.txt <alvo>` | Salva em formato grepável |

### tcpdump – Captura de pacotes (Linux)

| Comando | Descrição |
|---------|-----------|
| `tcpdump -i eth0` | Captura pacotes na interface eth0 |
| `tcpdump -i eth0 -c 100` | Captura apenas 100 pacotes |
| `tcpdump -i eth0 -w captura.pcap` | Salva captura em arquivo |
| `tcpdump -r captura.pcap` | Lê arquivo de captura salvo |
| `tcpdump -i eth0 port 80` | Captura apenas tráfego HTTP |
| `tcpdump -i eth0 src 192.168.1.10` | Captura apenas pacotes com origem específica |
| `tcpdump -i eth0 dst 192.168.1.10` | Captura apenas pacotes com destino específico |
| `tcpdump -i eth0 -n` | Não resolve nomes (mais rápido) |

### Wireshark – Filtros comuns

| Filtro | Descrição |
|--------|-----------|
| `http` | Mostra apenas tráfego HTTP |
| `tcp.port == 443` | Mostra tráfego na porta 443 (HTTPS) |
| `ip.src == 192.168.1.10` | Pacotes com IP de origem específico |
| `ip.dst == 192.168.1.10` | Pacotes com IP de destino específico |
| `tcp.flags.syn == 1` | Mostra pacotes com flag SYN (início de conexão) |
| `arp` | Mostra tráfego ARP |

### hping3 – Injeção de pacotes

| Comando | Descrição |
|---------|-----------|
| `hping3 -S <alvo> -p 80` | Envia pacote TCP SYN para porta 80 |
| `hping3 -A <alvo> -p 80` | Envia pacote TCP ACK para porta 80 |
| `hping3 -S <alvo> -p 80 --tcp-timestamp` | Inclui carimbo de data/hora |
| `hping3 --traceroute -S <alvo>` | Rastreamento de rota com TCP SYN |

### Outros comandos de rede

| Comando | Descrição |
|---------|-----------|
| `ping <alvo>` | Testa conectividade básica |
| `traceroute <alvo>` | Mostra rota até o destino (Linux) |
| `tracert <alvo>` | Mostra rota até o destino (Windows) |
| `netstat -tunap` | Mostra portas abertas e conexões ativas (Linux) |
| `netstat -an` | Mostra portas abertas e conexões (Windows) |
| `ss -tunap` | Alternativa moderna ao netstat (Linux) |
| `curl <url>` | Faz requisição HTTP simples |
| `curl -X POST -H "Content-Type: application/json" -d '{"chave":"valor"}' <url>` | Envia POST com JSON |
| `dig <dominio>` | Consulta DNS |
| `nslookup <dominio>` | Consulta DNS (Windows/Linux) |
| `whois <dominio>` | Consulta informações de registro de domínio |

---

## 🐧 Linux – Administração e Segurança

### Gerenciamento de serviços e processos

| Comando | Descrição |
|---------|-----------|
| `systemctl status <servico>` | Verifica status de um serviço |
| `systemctl start <servico>` | Inicia um serviço |
| `systemctl stop <servico>` | Para um serviço |
| `systemctl enable <servico>` | Habilita serviço na inicialização |
| `journalctl -xe` | Visualiza logs do sistema (systemd) |
| `ps aux` | Lista processos em execução |
| `ps aux \| grep <processo>` | Filtra processos específicos |
| `top` | Monitora processos em tempo real |
| `htop` | Versão melhorada do top |
| `kill -9 <PID>` | Força encerramento de processo |
| `lsof -i :<porta>` | Descobre qual processo está usando uma porta |

### Gerenciamento de usuários e permissões

| Comando | Descrição |
|---------|-----------|
| `sudo useradd -m <usuario>` | Cria novo usuário com diretório home |
| `sudo passwd <usuario>` | Define senha do usuário |
| `sudo userdel -r <usuario>` | Remove usuário e seu diretório home |
| `usermod -aG <grupo> <usuario>` | Adiciona usuário a um grupo |
| `chmod 750 <arquivo>` | Altera permissões (rwxr-x---) |
| `chown <usuario>:<grupo> <arquivo>` | Altera proprietário e grupo |
| `sudo visudo` | Edita configuração do sudoers (seguro) |

### Firewall (iptables/nftables/ufw)

| Comando | Descrição |
|---------|-----------|
| `sudo ufw status` | Verifica status do firewall (UFW) |
| `sudo ufw enable` | Ativa UFW |
| `sudo ufw allow 22/tcp` | Libera porta SSH |
| `sudo ufw deny 80/tcp` | Bloqueia porta HTTP |
| `sudo iptables -L -n -v` | Lista regras do iptables |
| `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT` | Adiciona regra de liberação de SSH |

### Logs e monitoramento

| Comando | Descrição |
|---------|-----------|
| `tail -f /var/log/syslog` | Acompanha logs do sistema em tempo real |
| `tail -f /var/log/auth.log` | Acompanha logs de autenticação |
| `grep "Failed password" /var/log/auth.log` | Busca tentativas de login falhas |
| `journalctl -u <servico> -f` | Acompanha logs de um serviço específico |
| `logrotate -f /etc/logrotate.conf` | Executa rotação de logs manualmente |

### Hardening básico

| Comando | Descrição |
|---------|-----------|
| `sudo apt update && sudo apt upgrade -y` | Atualiza sistema (Debian/Ubuntu) |
| `sudo yum update -y` | Atualiza sistema (RHEL/CentOS) |
| `sudo systemctl disable <servico>` | Desabilita serviço na inicialização |
| `sudo systemctl stop <servico>` | Para serviço imediatamente |

---

## 🪟 Windows – Administração e Segurança

### PowerShell – Comandos úteis

| Comando | Descrição |
|---------|-----------|
| `Get-Service` | Lista serviços em execução |
| `Stop-Service -Name <servico>` | Para um serviço |
| `Start-Service -Name <servico>` | Inicia um serviço |
| `Get-Process` | Lista processos em execução |
| `Stop-Process -Name <processo>` | Encerra um processo |
| `Get-WindowsUpdate` | Verifica atualizações disponíveis |
| `Install-WindowsUpdate` | Instala atualizações |
| `Get-NetFirewallRule` | Lista regras do firewall |
| `New-NetFirewallRule -DisplayName "Nome" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow` | Cria regra de firewall |
| `Get-ADUser -Filter *` | Lista usuários do Active Directory |
| `Get-ADGroup -Filter 'GroupCategory -eq "Security"'` | Lista grupos de segurança do AD |
| `New-ADGroup -Name "NOME" -GroupCategory Security -GroupScope DomainLocal` | Cria novo grupo de segurança |
| `Add-ADGroupMember -Identity "GRUPO" -Members "USUARIO"` | Adiciona usuário a um grupo |
| `Get-EventLog -LogName Security -Newest 50` | Lista últimos 50 eventos do log de segurança |

### Comandos CMD

| Comando | Descrição |
|---------|-----------|
| `ipconfig /all` | Mostra configurações de rede |
| `ipconfig /flushdns` | Limpa cache DNS |
| `ping <alvo>` | Testa conectividade |
| `tracert <alvo>` | Rastreamento de rota |
| `netstat -an` | Mostra portas abertas e conexões |
| `net user` | Lista usuários do sistema |
| `net localgroup administrators` | Lista membros do grupo Administradores |
| `sfc /scannow` | Verifica integridade de arquivos do sistema |
| `chkdsk /f` | Verifica e corrige erros no disco |
| `shutdown /r /t 0` | Reinicia imediatamente |
| `gpupdate /force` | Atualiza políticas de grupo |

---

## 🔑 Criptografia e Certificados

### OpenSSL – Comandos úteis

| Comando | Descrição |
|---------|-----------|
| `openssl genrsa -out chave_privada.pem 2048` | Gera chave privada RSA de 2048 bits |
| `openssl rsa -in chave_privada.pem -pubout -out chave_publica.pem` | Extrai chave pública da chave privada |
| `openssl req -new -key chave_privada.pem -out csr.pem` | Gera CSR (Certificate Signing Request) |
| `openssl x509 -req -in csr.pem -signkey chave_privada.pem -out certificado.pem -days 365` | Gera certificado autoassinado |
| `openssl x509 -in certificado.pem -text -noout` | Visualiza detalhes de um certificado |
| `openssl s_client -connect google.com:443 -showcerts` | Verifica certificado de um site HTTPS |
| `echo "mensagem" \| openssl dgst -sha256 -sign chave_privada.pem` | Assina digitalmente uma mensagem |
| `openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin mensagem.txt` | Verifica assinatura digital |

### Hash de arquivos

| Comando | Descrição |
|---------|-----------|
| `md5sum arquivo` | Calcula hash MD5 (Linux) – inseguro para senhas |
| `sha256sum arquivo` | Calcula hash SHA-256 (Linux) |
| `Get-FileHash arquivo -Algorithm SHA256` | Calcula hash SHA-256 (PowerShell) |
| `certutil -hashfile arquivo MD5` | Calcula hash MD5 (Windows CMD) |

---

## 🤖 Ansible – Automação

| Comando | Descrição |
|---------|-----------|
| `ansible all -m ping -i inventario.ini` | Testa conectividade com todos os hosts |
| `ansible <grupo> -m command -a "comando" -i inventario.ini` | Executa comando remoto |
| `ansible-playbook playbook.yml` | Executa um playbook |
| `ansible-playbook playbook.yml --check` | Modo "dry-run" (não aplica mudanças) |
| `ansible-playbook playbook.yml --ask-become-pass` | Solicita senha sudo durante execução |
| `ansible-vault encrypt arquivo.yml` | Criptografa arquivo sensível |
| `ansible-vault decrypt arquivo.yml` | Descriptografa arquivo |
| `ansible-doc -l` | Lista módulos disponíveis |
| `ansible-doc <modulo>` | Mostra documentação de um módulo |

---

## 🔐 Hashcat – Quebra de senhas

| Comando | Descrição |
|---------|-----------|
| `hashcat -m 0 -a 0 hash.txt wordlist.txt` | Ataque de dicionário (MD5) |
| `hashcat -m 1000 -a 3 hash.txt ?l?l?l?l?l?l?l?l` | Ataque com máscara (8 letras minúsculas) |
| `hashcat -m 1000 -a 3 hash.txt -1 ?l?u?d ?1?1?1?1?1?1?1?1` | Máscara com letras maiúsculas/minúsculas/números |
| `hashcat -m 1000 -a 0 hash.txt wordlist.txt -r regras.rule` | Ataque de dicionário com regras |
| `hashcat --stdout -a 3 ?d?d?d?d` | Gera todas combinações de 4 dígitos (saída padrão) |

**Tipos de hash comuns (-m):**
- `0` = MD5
- `1000` = NTLM (Windows)
- `1800` = sha512crypt (Linux)
- `5500` = NetNTLMv1
- `5600` = NetNTLMv2

---

## 📦 Git – Controle de versão

| Comando | Descrição |
|---------|-----------|
| `git clone <url>` | Clona repositório remoto |
| `git status` | Mostra arquivos modificados |
| `git add <arquivo>` | Adiciona arquivo ao staging |
| `git add .` | Adiciona todos os arquivos modificados |
| `git commit -m "mensagem"` | Cria commit com mensagem |
| `git push origin main` | Envia commits para o repositório remoto |
| `git pull origin main` | Atualiza repositório local com mudanças remotas |
| `git log --oneline` | Mostra histórico de commits resumido |
| `git diff` | Mostra diferenças entre arquivos modificados |
| `git branch` | Lista branches locais |
| `git checkout -b <branch>` | Cria e troca para nova branch |
| `git merge <branch>` | Mescla branch atual com outra branch |

---

## 🖥️ Virtualização (Vagrant)

| Comando | Descrição |
|---------|-----------|
| `vagrant init <box>` | Inicializa Vagrantfile com uma box |
| `vagrant up` | Sobe a VM (cria se não existir) |
| `vagrant ssh` | Conecta à VM via SSH |
| `vagrant halt` | Desliga a VM |
| `vagrant destroy` | Remove a VM |
| `vagrant reload` | Reinicia a VM (aplica alterações no Vagrantfile) |
| `vagrant status` | Mostra status da VM |
| `vagrant box list` | Lista boxes disponíveis localmente |
| `vagrant box update` | Atualiza a box da VM |

---

## 💡 Dicas rápidas

| Situação | Comando/Solução |
|----------|-----------------|
| Descobrir IP da máquina (Linux) | `ip a` ou `hostname -I` |
| Descobrir IP da máquina (Windows) | `ipconfig` |
| Testar conectividade com port específica | `nc -zv <alvo> <porta>` (Netcat) |
| Verificar se porta está ouvindo (Linux) | `ss -tlnp \| grep <porta>` |
| Verificar se porta está ouvindo (Windows) | `netstat -an \| findstr <porta>` |
| Matar processo por nome (Linux) | `pkill <nome>` |
| Matar processo por nome (Windows) | `taskkill /IM <nome.exe> /F` |
| Verificar espaço em disco (Linux) | `df -h` |
| Verificar espaço em disco (Windows) | `wmic logicaldisk get size,freespace,caption` |
| Verificar consumo de memória (Linux) | `free -h` |
| Verificar consumo de memória (Windows) | `Get-Counter "\Memory\Available MBytes"` |
| Buscar string em arquivos (Linux) | `grep -r "texto" /caminho` |
| Buscar string em arquivos (Windows) | `findstr /s "texto" *.*` |