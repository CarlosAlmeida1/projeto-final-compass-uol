# ☁️ Projeto final do programa de bolsas da Compass Uol

<div align="center">
    <img src="images/compass-uol.svg" width="310px" alt="Compass Uol Logo">
</div>

---

## 👥 Integrantes

- Carlos Henrique de Almeida Martins
- Nicole Evelyn Oliveira Profeta

---

## 🔍 Apresentação do projeto

A empresa "Fast Engineering S/A" está em busca de uma solução da empresa terceira "TI SOLUÇÕES INCRÍVEIS". O eCommerce da "Fast Engineering S/A" está em expansão e a solução atual não está mais suportando o aumento significativo de acessos e compras, que têm crescido 20% ao mês desde o início do ano.

### Tecnologias atuais

- 01 servidor para Banco de Dados MySQL
- 01 servidor para a aplicação utilizando REACT
- 01 servidor de web server que armazena estáticos como fotos e links

### Requisitos da Nova Arquitetura

Para a construção da arquitetura do futuro website da "Fast Engineering S/A", é necessário seguir as melhores práticas DevOps, incluindo:

- Ambiente Kubernetes
- Banco de dados PaaS
- MultiAZ
- Segurança de backup de dados
- Persistência dos dados
- Balanceamento de carga com healthcheck
- Segurança

---

## 📚 Documentação

### Arquitetura Atual

A arquitetura atual do eCommerce da "Fast Engineering S/A" é composta por 3 servidores, sendo um para o Banco de Dados MySQL, um para a aplicação utilizando REACT e um para o servidor de web server que armazena estáticos como fotos e links.

<div align="center">
    <img src="images/estrutura-atual.jpg" width="500px" alt="Arquitetura Atual">
</div>
<div align="center">
    <strong>Arquitetura Atual</strong>
</div>

### Cenário Atual (On-premise)

Ambiente com três servidores:

- Front-end Web: Interface para os clientes.
- Back-end API: Processa solicitações e gerencia lógica de negócios.
- Banco de Dados MySQL: Armazena informações críticas.

Comunicação:

- Clientes acessam o ambiente on-premise diretamente.

### Arquitetura De Migração

A arquitetura de migração proposta para o eCommerce da "Fast Engineering S/A" é composta por 3 servidores, sendo um para o Banco de Dados MySQL, um para a aplicação utilizando REACT e um para o servidor de web server que armazena estáticos como fotos e links. Será usado o MGN para a migração dos dados, DMS para a replicação dos dados e o RDS para o banco de dados. S3 para armazenamento de arquivos estáticos.

<div align="center">
    <img src="images/arquitetura-de-migracao.jpg" width="500px" alt="Arquitetura de Migração">
</div>
<div align="center">
    <strong>Arquitetura de Migração</strong>
</div>

#### Fluxo de Migração

#### Passo 1: Replicação de Dados

Replication Agent:

- Configurado no ambiente on-premise.
- Usa TCP 1500 (Data Transfer) para transferir dados para o Replication Server na AWS.

Replication Server:

- Hospedado na AWS dentro de uma VPC em uma subnet pública.
- Conecta-se ao EBS para armazenar os dados replicados.

#### Passo 2: Controle e Integração

O Replication Agent também usa:

- TCP 443 (Control Protocols) para comunicação com o AWS MGN.
- Envia dados ao Amazon S3 para backup.

#### Passo 3: Migração de Banco de Dados

O banco de dados on-premise utiliza TCP 3306 para enviar dados ao MGN na AWS:

- O MGN está em uma subnet privada de uma nova VPC.
- O MGN transfere os dados para o Amazon RDS.

### Nova Infraestrutura na AWS

#### Camada de Banco de Dados

Amazon RDS:

- Gerencia o banco de dados MySQL migrado.
- Conecta-se ao EC2 back-end.

#### Camada Back-end

EC2 back-end:

- Hospeda serviços: API, API2 e servidor Nginx.
- Conexão bidirecional com o EBS para armazenamento.
- Balanceamento de carga por meio de um Load Balancer.

#### Camada Front-end

Load Balancer:

- Distribui o tráfego para o EC2 back-end.
- Conecta-se ao EBS e ao EC2 front-end.

EC2 front-end:

- Interface web para os clientes.
- Comunicação bidirecional com o EBS.

### Arquitetura Moderna

---

## 🛠️ Serviços Utilizados

## Implementação
