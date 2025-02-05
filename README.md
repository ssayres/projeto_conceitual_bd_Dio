# projeto_conceitual_bd_Dio
Refinando um projeto conceitual de banco de dados

1. Contexto: Levantamento de Requisitos

A Universidade necessita de um sistema de banco de dados para gerenciar clientes (Pessoa Física e Jurídica), formas de pagamento e entregas de produtos ou serviços acadêmicos. O sistema deve atender aos seguintes requisitos:

Requisitos Funcionais

Um cliente pode ser Pessoa Física (PF) ou Pessoa Jurídica (PJ), mas nunca ambos.

Um cliente pode possuir múltiplas formas de pagamento cadastradas.

O sistema deve registrar todas as entregas realizadas, incluindo status da entrega e código de rastreamento.

Requisitos Não Funcionais

O banco de dados deve ser modelado para garantir integridade referencial.

O acesso às informações deve ser seguro e rápido.

O modelo deve permitir escalabilidade para futuras expansões.

2. Projeto Conceitual - Modelo Entidade-Relacionamento (ER)

O modelo ER foi desenvolvido para representar as entidades e seus relacionamentos.

Entidades e Atributos

Cliente (PK id_cliente)

Nome

Tipo (PF/PJ)

CPF (se PF)

CNPJ (se PJ)

Email

Telefone

Forma de Pagamento (PK id_pagamento)

Tipo (Cartão de Crédito, Boleto, Transferência)

Detalhes

FK para Cliente

Entrega (PK id_entrega)

Status (Pendente, Em Transporte, Entregue, Cancelado)

Código de Rastreio

Data da Entrega

FK para Cliente

Relacionamentos

Um cliente pode ter múltiplas formas de pagamento.

Um cliente pode ter múltiplas entregas registradas.


Tabela e Estruturas 

CREATE TABLE Cliente (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(255) NOT NULL,
    tipo ENUM('PF', 'PJ') NOT NULL,
    cpf VARCHAR(11) UNIQUE NULL,
    cnpj VARCHAR(14) UNIQUE NULL,
    email VARCHAR(255) NOT NULL,
    telefone VARCHAR(20)
);

CREATE TABLE Forma_Pagamento (
    id_pagamento INT PRIMARY KEY AUTO_INCREMENT,
    tipo ENUM('Cartao', 'Boleto', 'Transferencia') NOT NULL,
    detalhes TEXT,
    id_cliente INT,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente) ON DELETE CASCADE
);

CREATE TABLE Entrega (
    id_entrega INT PRIMARY KEY AUTO_INCREMENT,
    status ENUM('Pendente', 'Em Transporte', 'Entregue', 'Cancelado') NOT NULL,
    codigo_rastreio VARCHAR(50) UNIQUE NOT NULL,
    data_entrega DATE,
    id_cliente INT,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente) ON DELETE SET NULL
);
