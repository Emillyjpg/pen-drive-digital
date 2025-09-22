# 📂 Pen Drive Digital – Servidor de Armazenamento Didático
## 📖 Visão Geral
Este projeto implementa um **servidor de armazenamento em rede (NAS)** utilizando **Linux Debian** e ferramentas como **TrueNAS** e **OpenMediaVault**. O sistema permite que usuários (alunos e professores) acessem e compartilhem arquivos de forma organizada, com controle de permissões e autenticação por login e senha.

--- 
## 🛠️ Tecnologias Utilizadas
- **Sistema Operacional:** Linux Debian
- **NAS:** TrueNAS, OpenMediaVault
- **Serviços de Rede:** Samba (SMB), FTP
- **Hardware:** Servidor físico (Storage/Desktop)
- **Alternativa em Nuvem:** Azure, AWS

--- 
## ⚙️ Implementação

### 1. Instalação do Servidor
Preparação do ambiente em **Linux Debian**, configuração inicial de rede (endereçamento IP e hostname) e instalação do **TrueNAS/OpenMediaVault** para gerenciar o servidor.
sudo apt update && sudo apt upgrade -y
sudo apt install samba

### 2. Estrutura de Diretórios
A organização de pastas foi criada para separar uso individual e coletivo, garantindo que professores, alunos e arquivos compartilhados tenham seus próprios espaços e controles de acesso:
/home/servidor/
 ├── Professores/
 │    ├── Materiais/
 │    └── Relatorios/
 ├── Alunos/
 │    ├── aluno01/
 │    ├── aluno02/
 │    └── ...
 ├── Compartilhado/
 │    └── ArquivosDidaticos/
Professores: acesso restrito por login.  
Alunos: cada um possui sua pasta privada.  
Compartilhado: materiais acessíveis a todos.

### 3. Controle de Usuários
Cada usuário recebe login e senha individuais para acessar o servidor de forma segura. As permissões são configuradas para que pastas privadas tenham acesso exclusivo e pastas públicas possam ser lidas e escritas por todos.
sudo adduser aluno01
sudo smbpasswd -a aluno01

### 4. Compartilhamento de Arquivos
Configuração do arquivo **smb.conf** para gerenciar permissões e controlar quem pode acessar cada pasta:
[Compartilhado]
   path = /home/servidor/Compartilhado
   browseable = yes
   writable = yes
   guest ok = no
   valid users = @usuarios

### 5. Dashboard de Gerenciamento
Com o OpenMediaVault ou TrueNAS, é possível administrar o servidor via interface gráfica, facilitando tarefas como criação e exclusão de usuários, gerenciamento de permissões, monitoramento de consumo de armazenamento e criação de backups.
![Dashboard do Servidor](imagens/dashboard.png)

### 6. Segurança e Políticas
Autenticação obrigatória via login e senha. Termo de uso definido para evitar armazenamento de mídias não didáticas. Possibilidade de integração com Active Directory (AD) para ambientes maiores. Backup planejado com RAID e cópias externas, garantindo integridade e segurança dos dados.

### 7. Possibilidades de Expansão
Acesso remoto via FTP ou VPN para administração e uso à distância. Integração com nuvem (Azure/AWS) para redundância e armazenamento seguro. Uso corporativo para organização de dados internos, centralização de arquivos e distribuição de atualizações.

### 8. Exemplos Visuais
Adicione prints reais da implementação para ilustrar a estrutura e configuração:
![Estrutura de Pastas](imagens/pastas.png)
![Configuração Samba](imagens/samba.png)
![Compartilhamento de Arquivos](imagens/compartilhamento.png)

### 9. Guia Rápido de Instalação
Atualizar o sistema, instalar o Samba, criar diretórios e usuários, configurar permissões e reiniciar o serviço:
sudo apt update && sudo apt upgrade -y  
sudo apt install samba  
mkdir -p /home/servidor/Compartilhado  
mkdir -p /home/servidor/Alunos/aluno01  
sudo adduser aluno01  
sudo smbpasswd -a aluno01  
sudo systemctl restart smbd

### 10. Acessar via rede no Windows
Para acessar o servidor a partir de um computador Windows, utilize o endereço de rede do compartilhamento:
\\ip-do-servidor\Compartilhado

📌 Este repositório demonstra a implementação prática de um servidor de arquivos em rede, com foco em segurança, organização e escalabilidade.

---
