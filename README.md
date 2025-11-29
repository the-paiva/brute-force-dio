# Estudo de Cibersegurança – Resumo sobre Kali Linux e Ataques Brute Force

## 1. Introdução ao Kali Linux
Kali Linux é uma distribuição baseada em Debian voltada para testes de penetração, análise forense e segurança ofensiva. Ele já vem com centenas de ferramentas pré-instaladas, divididas em categorias como:
- *Information Gathering*
- *Vulnerability Analysis*
- *Exploitation Tools*
- *Password Attacks*
- *Web Application Analysis*
- *Wireless Attacks*, entre outras.

Seu foco é facilitar o uso de ferramentas de ataque, automatizar processos e criar um ambiente completo para pesquisa de segurança.

---

## 2. Ataques Brute Force
O **brute force attack** (também conhecido como **ataque de força bruta**) consiste em tentar repetidamente combinações de credenciais (usuário/senha) até encontrar a correta.  
É um ataque ruidoso, fácil de detectar, mas ainda muito usado quando:

- Não existe bloqueio por tentativas.
- A senha é fraca.
- O atacante tem acesso a wordlists completas.

### Tipos comuns:
- **Brute Force tradicional** – testa todas as combinações possíveis.
- **Dictionary Attack** – usa listas pré-prontas de palavras.
- **Password Spraying** – usa *uma senha* contra *vários usuários*, evitando bloqueio por falhas consecutivas.
- **Credential Stuffing** – usa senhas vazadas reutilizadas pelo usuário.

---

## 3. Ferramentas do Kali Linux estudadas

### 3.1 Nmap
Ferramenta de *network scanning* e *enumeration*.  
Permite:
- Mapear portas abertas
- Identificar serviços
- Verificar versões
- Detecção de sistemas operacionais  
Exemplo:
```
nmap -sV -A 192.168.0.10
```

---

### 3.2 Medusa
Ferramenta rápida de brute force em serviços de autenticação.  
Permite ataques paralelos a protocolos como FTP, SSH, SMB, HTTP, etc.

Exemplo:
```
medusa -h 192.168.0.10 -u admin -P /usr/share/wordlists/rockyou.txt -M ssh
```

---

### 3.3 Ncrack
Voltada para ataques rápidos e modulares de brute force, focada em alta performance.  
Indicado para:
- RDP
- SSH
- FTP
- WinRM  
Exemplo:
```
ncrack -p ssh 192.168.0.10 -u root -P rockyou.txt
```

---

### 3.4 John the Ripper (JtR)
Ferramenta para **quebra de hashes**, muito usada após obter arquivos de senhas.  
Funciona com vários tipos de hash: MD5, SHA1, NTLM, bcrypt, etc.

Etapas comuns:
1. Extrair hash
2. Colocar em um arquivo `.txt`
3. Executar o John  
Exemplo:
```
john senha.hash
```

---

### 3.5 WPScan
Ferramenta específica para **WordPress**.  
Permite:
- Enumerar usuários
- Identificar vulnerabilidades de plugins e temas
- Realizar brute force em logins WP

Exemplo:
```
wpscan --url http://alvo.com --passwords rockyou.txt --usernames admin
```

---

### 3.6 Patator
Ferramenta flexível e modular para brute force e fuzzing.  
Vantagens:
- Suporte a muitos protocolos
- Customização do fluxo de ataque
- Controle sobre threads e timeouts  
Exemplo:
```
patator ssh_login host=192.168.0.10 user=admin password=FILE0 0=rockyou.txt
```

---

### 3.7 smbclient
Cliente que possibilita interação com compartilhamentos SMB/Samba.  
Ajuda na:
- Enumeração
- Listagem de diretórios
- Download de arquivos  
Exemplo:
```
smbclient -L 192.168.0.10 -N
```

---

### 3.8 Metasploitable 2
Máquina virtual vulnerável usada como alvo de testes.  
Possui falhas em serviços como:
- FTP
- SSH
- Tomcat
- Samba
- MySQL

Serve como laboratório seguro para:
- Exploit
- Post-exploitation
- Brute force realista

---

### 3.9 Wordlists
Conjuntos de palavras usados em ataques de senha. O Kali inclui diversas listas em:
```
/usr/share/wordlists
```
A mais famosa:
- **rockyou.txt** – contém milhões de senhas reais vazadas.

Também é possível criar wordlists personalizadas com:
```
cewl
crunch
```

---

## 4. Password Spraying
Técnica que tenta **uma senha muito provável** contra **vários usuários**.  
Evita bloqueios por tentativas consecutivas falhas.

Exemplo de cenário:
- Lista de usuários corporativos.
- Uma senha comum: `Senha123!`
- Testar a mesma senha em todos os usuários.

---

# Conclusão
Para um profissional de cibersegurança é **essencial** compreender ferramentas e técnicas de brute force, scanning e enumeração para entender como invasores agem — e, principalmente, como defender sistemas.  
O Kali Linux oferece um ambiente completo para estudos ofensivos de forma ética e controlada.
