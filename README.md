# PetLog – Sistema de Gestão Completo para Petshops

O **PetLog** é uma solução web full-stack desenvolvida para otimizar a gestão de petshops, abrangendo o controle de clientes, animais de estimação e o agendamento de serviços. Com uma interface intuitiva em HTML/CSS/JavaScript e um robusto back-end construído na AWS Lambda, API Gateway e DynamoDB, o PetLog oferece uma plataforma eficiente e escalável para o seu negócio.

---

## Destaques do Projeto

- **Gestão Abrangente:** Controle completo de clientes, pets e agendamentos.  
- **Integração AWS:** Utiliza serviços serverless da AWS para alta disponibilidade e escalabilidade.  
- **Interface Amigável:** Design limpo e responsivo para uma ótima experiência do usuário.  
- **Validações Robustas:** Garante a integridade dos dados com validações em tempo real.

---

## Tecnologias Utilizadas

### Front-end

- **HTML5:** Estrutura e semântica das páginas.  
- **CSS3:** Estilização e responsividade da interface.  
- **JavaScript Vanilla:** Lógica de interação, chamadas à API e manipulação do DOM.

### Back-end

- **Python 3.x:** Linguagem de programação para as funções Lambda.  
- **AWS Lambda:** Funções serverless para execução do código de back-end.  
- **AWS API Gateway:** Criação e gerenciamento de endpoints RESTful para as funções Lambda.  
- **Amazon DynamoDB:** Banco de dados NoSQL para persistência dos dados (clientes, animais, agendamentos, contas).  
- **Boto3:** SDK oficial da AWS para Python, utilizado para interagir com o DynamoDB.

---

## Funcionalidades Implementadas

O PetLog oferece um conjunto de funcionalidades essenciais para a gestão de um petshop:

### Usuários e Contas

- Cadastro de contas (registro de novos usuários) – `contas_post.py`  
- Login e autenticação simples para ADMIN – `login.html`, `contas_get_from_user.py`  
- Gerenciamento de contas (alteração e exclusão) – `contas_alter.py`, `contas_delete.py`  
- Consulta de contas – `contas_get_from_user.py`

### Clientes

- Cadastro de clientes – `cadastro.html`, `clientes_post.py`  
- Listagem de clientes – `listacad.html`, `clientes_get_all.py`  
- Consulta de clientes por nome ou userId – `clientes_get_from_cliente.py`, `clientes_get_by_userId.py`  
- Atualização e remoção de clientes – `clientes_alter.py`, `clientes_delete.py`

### Animais

- Cadastro de animais (associados a dono e conta) – `cadastro_pet.html`, `animais_post.py`  
- Consulta de animais por nome, dono ou userId – `animais_get_by_nome.py`, `animais_get_by_dono.py`, `animais_get_by_conta.py`  
- Edição e exclusão de animais – `animais_alter.py`, `animais_delete.py`

### Agendamentos

- Criação de agendamentos de serviços – `agenda.html`, `agenda_post.py`  
- Consulta de agendamentos por data ou dono – `agenda_get_by_data.py`, `agenda_get_by_dono.py`  
- Alteração e cancelamento de agendamentos – `agenda_alter.py`, `agenda_delete.py`

### Validações

- As operações de criação e alteração no back-end incluem validações para garantir a existência de `userId`, `owner` (dono) e `animal` antes de registrar agendamentos ou pets.

---

## Estrutura do Projeto

petlog/
├── frontend/
│ ├── agenda.html # Interface para agendamentos
│ ├── animais.html # Interface para consulta e gestão de animais
│ ├── cadastro.html # Formulário de cadastro de clientes
│ ├── cadastro_pet.html # Formulário de cadastro de pets
│ ├── listacad.html # Lista de clientes cadastrados
│ ├── login.html # Página de login do sistema
│ └── sistema.html # Dashboard principal do sistema
│
├── backend/
│ ├── agenda_alter.py # Função Lambda para alterar agendamentos
│ ├── agenda_delete.py # Função Lambda para excluir agendamentos
│ ├── agenda_get_by_data.py # Função Lambda para buscar agendamentos por data
│ ├── agenda_get_by_dono.py # Função Lambda para buscar agendamentos por dono
│ ├── agenda_post.py # Função Lambda para criar agendamentos
│
│ ├── animais_alter.py # Função Lambda para alterar dados de animais
│ ├── animais_delete.py # Função Lambda para excluir animais
│ ├── animais_get_by_conta.py # Função Lambda para buscar animais por userId
│ ├── animais_get_by_dono.py # Função Lambda para buscar animais por dono
│ ├── animais_get_by_nome.py # Função Lambda para buscar animais por nome
│ ├── animais_post.py # Função Lambda para criar animais
│
│ ├── clientes_alter.py # Função Lambda para alterar clientes
│ ├── clientes_delete.py # Função Lambda para excluir clientes
│ ├── clientes_get_all.py # Função Lambda para listar todos os clientes
│ ├── clientes_get_by_userId.py # Função Lambda para buscar clientes por userId
│ ├── clientes_get_from_cliente.py # Função Lambda para buscar cliente por nome
│ ├── clientes_post.py # Função Lambda para criar clientes
│
│ ├── contas_alter.py # Função Lambda para alterar contas (usuários)
│ ├── contas_delete.py # Função Lambda para excluir contas (usuários)
│ ├── contas_get_from_user.py # Função Lambda para buscar conta por nome de usuário
│ └── contas_post.py # Função Lambda para criar contas (usuários)
│
├── .gitignore # Arquivos ignorados pelo Git
└── README.md # Este arquivo


**Obs:** Cada script Python no diretório `backend/` corresponde a uma função AWS Lambda que deve ser configurada e conectada a um endpoint no AWS API Gateway.

---

## Como Executar o Projeto (Guia de Implantação)

### 1. Configuração do Banco de Dados (DynamoDB)

- Crie as seguintes tabelas no Amazon DynamoDB:  
  - `table_agenda` (chave primária: Id)  
  - `table_animais` (chave primária: Id)  
  - `table_clientes` (chave primária: Nome)  
  - `table_contas` (chave primária: User)  
- Certifique-se que os nomes usados no código Python (`dynamodb.Table('table_...')`) correspondam exatamente aos nomes das tabelas criadas.

### 2. Implantação das Funções Lambda (AWS Lambda)

- Para cada arquivo `.py` no diretório `backend/`, crie uma função Lambda na AWS.  
- Use Python 3.x como runtime.  
- Configure permissões IAM para que as funções possam acessar o DynamoDB (leitura e escrita).  
- Faça upload do código para cada função correspondente.

### 3. Configuração da API (AWS API Gateway)

- Crie uma API REST no AWS API Gateway.  
- Para cada função Lambda, crie recursos e métodos HTTP correspondentes (ex: POST /agenda para `agenda_post.py`).  
- Integre cada método com a função Lambda adequada.  
- Habilite CORS para permitir acesso do frontend.

### 4. Atualização das URLs no Frontend

- Após a implantação, você receberá o "Invoke URL" da API Gateway.  
- Atualize os arquivos HTML (`agenda.html`, `animais.html`, `cadastro.html`, `cadastro_pet.html`) substituindo as URLs placeholders pelos seus endpoints reais.

### 5. Hospedagem do Frontend

- Hospede os arquivos HTML em um bucket S3 configurado para site estático, ou abra-os localmente no navegador para testes.

---

## Segurança e Boas Práticas

- **Variáveis de Ambiente:** Use variáveis de ambiente para configurações sensíveis, evitando hardcoding.  
- **Políticas IAM Granulares:** Defina permissões mínimas necessárias para cada função Lambda.  
- **Gerenciamento de Segredos:** Utilize AWS Secrets Manager para dados sensíveis além de variáveis de ambiente.  
- **Validações de Entrada:** Reforce a validação e sanitização das entradas para evitar vulnerabilidades (ex: injeção).

---

## Status do Projeto

- Em desenvolvimento: funcionalidades principais de agendamento, gestão de clientes e animais, e gerenciamento básico de contas já implementadas.

---

## Próximas Melhorias Planejadas

- Sistema de login e autenticação robusto (ex: AWS Cognito).  
- Upload e armazenamento de fotos de pets usando AWS S3.  
- Dashboard interativo com gráficos e relatórios.  
- Sistema de notificações (SMS/Email) para agendamentos.

---

## Autor

**Gustavo**  
Estudante de Análise e Desenvolvimento de Sistemas  
Email: [Seu Email Aqui]  
LinkedIn / GitHub / Portfólio: [Seu Link Aqui]

---

## Licença

Este projeto é disponibilizado para fins educacionais. Sinta-se à vontade para estudar, modificar e usar como base para seus próprios projetos.
