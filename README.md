# Secure Remote Access Lab 

Este projeto documenta a implementação de um laboratório Linux focado em segurança defensiva e controle de acesso remoto. O objetivo foi configurar um servidor acessível via internet, mas protegido contra ataques de força bruta e scans automáticos.

# O Desafio
O laboratório foi construído para estabelecer um ambiente de estudos seguro, enfrentando os seguintes desafios:
* **Exposição Direta:** Necessidade de abrir portas para acesso remoto via internet.
* **Ataques de Brute Force:** Proteção contra bots que testam senhas e usuários comuns.
* **Autenticação Robusta:** Eliminar a fragilidade de senhas tradicionais.

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
Screenshot 
<img width="784" height="25" alt="image" src="https://github.com/user-attachments/assets/440ffba3-3157-4f78-b437-d523846448e0" />

