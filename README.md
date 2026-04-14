# Secure Remote Access Lab 

Este projeto documenta a implementação de um laboratório Linux focado em segurança defensiva e controle de acesso remoto. O objetivo foi configurar um servidor acessível via internet, mas protegido contra ataques de força bruta e scans automáticos.

# O Desafio
O laboratório foi construído para estabelecer um ambiente de estudos seguro, enfrentando os seguintes desafios:
* **Exposição Direta:** Necessidade de abrir portas para acesso remoto via internet.
* **Ataques de Brute Force:** Proteção contra bots que testam senhas e usuários comuns.
* **Autenticação Robusta:** Eliminar a fragilidade de senhas tradicionais.
* **Problema:** O provedor de internet não fornece um IP público real para o roteador, impossibilitando o redirecionamento de portas (Port Forwarding) tradicional.
* **Motivação:** A utilização da VM na Azure surgiu como a solução para atuar como um **Bastion Host**, permitindo que o laboratório seja acessível de qualquer lugar, contornando a limitação do IP compartilhado do provedor.

# Solução Implementada
A segurança do ambiente foi baseada em camadas de **Hardening**:

1.  **SSH Port Obfuscation:** Alteração da porta padrão do SSH para a `2222`.
2.  **Key-Based Authentication:** Desativação total de senhas. Acesso permitido apenas através de chaves criptográficas.
3.  **Defesa Ativa com Fail2Ban:** Implementação de banimento automático de IPs maliciosos.

---

# Configurações Principais

### 1. SSH Hardening (`/etc/ssh/sshd_config`)
As seguintes diretivas foram aplicadas para restringir o acesso:

```bash
Port 2222                     # Porta personalizada
PasswordAuthentication no     # Bloqueia login por senha
PubkeyAuthentication yes      # Permite apenas chaves públicas
PermitRootLogin no            # Proíbe acesso direto como root
MaxAuthTries 3                # Limita tentativas de login
```

Screenshot

<img width="784" height="25" alt="image" src="https://github.com/user-attachments/assets/c14b88b3-67f0-4b49-94b1-41c4f2539e7b" />

# Configuração do monitoramento agressivo para detectar erros de login:

```bash
Ini, TOML
[sshd]
enabled = true
port    = 2222
filter  = sshd
mode    = aggressive
maxretry = 3
bantime  = 1d
```
Screenshot

<img width="512" height="190" alt="image" src="https://github.com/user-attachments/assets/b3ceeb78-54d5-4837-8edb-c5942e118491" />

# Camadas de Segurança (Deep Dive)
Fail2Ban (Modo Aggressive): Diferente do modo padrão, o modo agressivo captura tentativas que falham logo no início (fase de publickey), banindo o atacante no Firewall (UFW) antes que ele possa testar outros usuários.

Firewall (UFW): Configurado para permitir tráfego apenas na porta específica do laboratório, negando todo o restante por padrão.

Log Monitoring: Monitoramento em tempo real do arquivo /var/log/auth.log para identificação de padrões de ataque.
# Tecnologias Utilizadas
OS: Ubuntu Server

Cloud: Microsoft Azure

Security: Fail2Ban (Advanced Mode), SSH Keys, UFW

Monitoramento: Netstat, Journalctl, Logwatch




