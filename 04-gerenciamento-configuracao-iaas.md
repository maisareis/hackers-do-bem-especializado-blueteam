# Aula 4 – Gerenciamento de Configuração e Infraestrutura como Serviço

## 📌 SOA – Arquitetura Orientada a Serviços
Abordagem que organiza sistemas em **serviços independentes e reutilizáveis**, cada um com uma função específica, que se comunicam por interfaces padronizadas. Permite atualizar ou substituir um componente sem derrubar o sistema inteiro.

**Microsserviços:** implementação prática da SOA. Cada serviço é ainda mais granular – pode ser desenvolvido, implantado e escalado de forma independente. Muito usado em ambientes cloud.

| | Monolito | Microsserviços |
|-|----------|----------------|
| Atualização | Afeta tudo | Afeta só o serviço |
| Escalabilidade | Escala o todo | Escala o que precisar |
| Falha | Derruba tudo | Isola no serviço |

---

## 📌 SOAP
Protocolo de comunicação entre sistemas distribuídos baseado em XML. Define um "envelope" padronizado com cabeçalho (autenticação, metadados) e corpo (dados da requisição/resposta). Muito usado em ambientes corporativos onde segurança e confiabilidade são críticos.

---

## 📌 SAML
Linguagem de marcação para autenticação e autorização em ambientes distribuídos. Base das soluções de **SSO (Single Sign-On)** – o usuário autentica uma vez e acessa vários sistemas sem precisar logar de novo.

---

## 📌 REST e APIs
**REST:** arquitetura para construir serviços web usando HTTP. Simples, escalável, amplamente adotada. Usa métodos como GET, POST, PUT e DELETE.

**APIs:** interfaces que permitem que sistemas se comuniquem. São porta de entrada para dados e funcionalidades.

**⚠️ APIs são um alvo frequente de ataques:**
- Falta de autenticação/autorização adequada
- Configurações incorretas
- Vulnerabilidades de código na implementação
- Ataques de injeção, negação de serviço, acesso a dados não autorizados

**Boas práticas de segurança em APIs:**
- Autenticação robusta (tokens, API keys, OAuth)
- Criptografia dos dados em trânsito
- Testes de segurança regulares
- Manter dependências e bibliotecas atualizadas

**Curl:** ferramenta de linha de comando para testar requisições HTTP/HTTPS. Muito útil para interagir com APIs durante testes.

---

## 📌 Automação e Scripting
Scripts automatizam tarefas repetitivas, reduzem erros humanos e aceleram processos. Linguagens comuns: Python, Bash, PowerShell.

Aplicações no Blue Team: configuração automatizada de servidores, coleta de logs, resposta a incidentes, testes de segurança.

---

## 📌 CI/CD, DevOps e DevSecOps

**CI (Integração Contínua):** desenvolvedores integram código no repositório frequentemente. Erros são detectados cedo.

**CD (Entrega Contínua):** o código vai automaticamente para produção após passar nos testes.

**DevOps:** derruba a barreira entre desenvolvimento e operações. Ciclos mais curtos, entregas mais frequentes.

**DevSecOps:** segurança integrada desde o início do desenvolvimento, não como etapa final. A ideia: "shift left" – antecipar os controles de segurança para as fases mais cedo possível.

---

## 📌 IaC – Infraestrutura como Código
Definir e provisionar infraestrutura usando arquivos de configuração (código), não de forma manual. Benefícios:
- Reproduzibilidade → mesmo ambiente em qualquer lugar
- Versionamento → controla mudanças como qualquer código
- Redução de erros humanos

---

## 📌 SOAR – Orquestração de Segurança, Automação e Resposta
Plataforma que integra ferramentas de segurança num fluxo de trabalho automatizado para resposta a incidentes. Combina automação com inteligência artificial para agir mais rápido que um humano conseguiria manualmente.

---

## 📌 FaaS / Serverless
Modelo cloud onde você escreve funções individuais que são executadas em resposta a eventos específicos. A plataforma gerencia a infraestrutura – você só se preocupa com o código. Escalabilidade automática e pagamento por uso.

---

## 💡 Meus Insights
- **APIs como superfície de ataque:** Fez sentido imediato. Toda integração moderna usa API. Se a API não tem autenticação correta, é a porta dos fundos que o atacante vai usar.
- **DevSecOps:** "Shift left" é o conceito mais importante aqui. Segurança no final do desenvolvimento é cara e ineficaz. No início, é muito mais barato corrigir.
- **IaC:** Percebi que isso se conecta diretamente com gerenciamento de configuração. Se a infraestrutura é código, ela pode ter controle de versão, revisão e rollback – exatamente como qualquer software.
- **SOAR:** A ideia de automatizar a resposta a incidentes é poderosa, mas também me gerou uma dúvida: até que ponto confiar em automação sem supervisão humana? E se o SOAR reagir errado?
- **Dúvida:** Quais ferramentas de IaC são mais usadas no mercado de segurança defensiva? Terraform? Ansible? Ambos?
