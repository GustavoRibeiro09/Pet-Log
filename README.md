#  PetLog – Sistema de Gestão de Petshop

O **PetLog** é uma aplicação web desenvolvida para facilitar a gestão de petshops, permitindo o controle de clientes, pets, agendamentos e serviços. Com integração a serviços da AWS, o sistema garante escalabilidade e alta disponibilidade.

---

##  Funcionalidades

- Cadastro e gerenciamento de clientes
- Registro de pets por cliente
- Agendamento de serviços (banho, tosa, consultas, etc.)
- Histórico de atendimentos
- Autenticação de usuários
- Integração com serviços da AWS (como S3, EC2, etc.)

---

##  Tecnologias Utilizadas

- **Front-end:** HTML5, CSS3, JavaScript
- **Back-end:** Node.js / Express (ou linguagem que estiver usando)
- **Banco de Dados:** MySQL / PostgreSQL (ou outro)
- **Cloud:** Amazon Web Services (AWS)
    - S3 para armazenamento
    - EC2 para hospedagem

---

## 🖥 Como Rodar o Projeto Localmente

```bash
# 1. Clone o repositório
git clone https://github.com/seu-usuario/petlog.git

# 2. Acesse a pasta do projeto
cd petlog

# 3. Instale as dependências
npm install

# 4. Configure as variáveis de ambiente
# Crie um arquivo .env e preencha com os dados necessários

# 5. Inicie o servidor
npm start

