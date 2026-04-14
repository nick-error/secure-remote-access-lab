# Secure Remote Access Lab 

Este projeto documenta a implementação de um laboratório Linux focado em segurança defensiva e controle de acesso remoto. O objetivo foi configurar um servidor acessível via internet, mas protegido contra ataques externos.

# O Desafio
O laboratório foi construído para estabelecer um ambiente de estudos seguro, enfrentando os seguintes desafios:
* **Exposição Direta:** Necessidade de abrir portas para acesso remoto via internet.
* **Ataques de Brute Force:** Proteção contra bots e scanners automáticos.
* **Autenticação Robusta:** Eliminar a fragilidade de senhas tradicionais.

# Solução Implementada
A segurança do ambiente foi baseada em camadas de **Hardening**:

1.  **SSH Port Obfuscation:** Alteração da porta padrão do SSH para a `2222` para reduzir o ruído de ataques automáticos.
2.  **Key-Based Authentication:** Desativação total de senhas. Acesso permitido apenas através de chaves criptográficas RSA/Ed25519.
3.  **SSH Hardening:** Configuração do `sshd_config` para ignorar tentativas de login inseguras.
4.  **Defesa Ativa com Fail2Ban:** Implementação de banimento automático de IPs maliciosos.

# Camadas de Segurança (Deep Dive)
* **Fail2Ban (Modo Aggressive):** Configurado para detectar e banir até mesmo tentativas que falham na fase de `publickey`, garantindo que o atacante seja bloqueado no Firewall antes mesmo de tentar novas conexões.
* **Firewall (UFW):** Configurado para permitir tráfego apenas na porta específica do laboratório.
* **Log Monitoring:** Monitoramento em tempo real do `auth.log` para identificação de padrões de ataque.
* Screenshot do status do Fail2ban
<img width="1110" height="215" alt="image" src="https://github.com/user-attachments/assets/c211058a-d13d-4735-ae38-d1acb1b7be96" />

# Tecnologias Utilizadas
* **OS:** Ubuntu Server
* **Security:** Fail2Ban (Advanced Mode), SSH Keys, UFW
* **Monitoramento:** Netstat, Journalctl


