# ProjetoCafeteria
Projeto banco de dados (Gestão de Cafeteria)

## Criação das tabelas modelo ER segue o código é só rodar no https://dbdiagram.io após precisamos conferir juntos as chaves e ligações 


Table cliente {
  id_cliente integer [primary key]
  nm_cliente varchar
  telefone char
  cpf char
}

Table mesa {
  id_mesa varchar [primary key]
  qtde_lugares tinyint
  status char(1)
  ambiente char(1)
}

Table comanda {
  id_comanda int [primary key]
  datahora_saida datetime
  id_mesa varchar
  id_cliente integer
  id_pedido integer
  id_funcionario integer
  }

  Table cardapio {
  id_cardapio integer [primary key]
  valor numeric
  nome varchar(80)
  classe_produto char(1)
}

Table pedidos {
  id_pedido integer [primary key]
  id_comanda integer
  id_cardapio integer
  qtde tinyint
  }

  Table cardapio_itens {
  cardapio_itens int [primary key]
  nome varchar(80)
  qtde tinyint
  id_cardapio integer
  }

  Table funcionario {
  id_funcionario integer [primary key]
  nome_funcionario varchar(50)
  cargo varchar(50)
  salario numeric
}

Table pagamento {
  id_pagamento integer [primary key]
  id_comanda int
  valor_pago numeric
  data_pagamento datetime
  }

Ref: "mesa"."id_mesa" < "comanda"."id_mesa"

Ref: "cliente"."id_cliente" < "comanda"."id_cliente"

Ref: "comanda"."id_pedido" < "pedidos"."id_pedido"

Ref: "comanda"."id_comanda" < "pedidos"."id_comanda"

Ref: "cardapio"."id_cardapio" < "pedidos"."id_cardapio"

Ref: "cardapio"."id_cardapio" < "cardapio_itens"."id_cardapio"

Ref: "comanda"."id_funcionario" < "funcionario"."id_funcionario"

Ref: "pagamento"."id_pagamento" < "comanda"."id_comanda"


## Atualizando criação das tabelas adicionado mais 2 tabelas  

-- Tabela cliente
CREATE TABLE cliente (
    id_cliente INTEGER PRIMARY KEY,
    nm_cliente VARCHAR(50),
    telefone CHAR(11),
    cpf CHAR(11)
);

-- Tabela mesa
CREATE TABLE mesa (
    id_mesa VARCHAR PRIMARY KEY,
    qtde_lugares TINYINT,
    status CHAR(1),
    ambiente CHAR(1)
);

-- Tabela comanda
CREATE TABLE comanda (
    id_comanda INT PRIMARY KEY,
    datahora_saida DATETIME,
    id_mesa VARCHAR,
    id_cliente INTEGER,
    id_pedido INTEGER
);

-- Tabela cardapio
CREATE TABLE cardapio (
    id_cardapio INTEGER PRIMARY KEY,
    valor NUMERIC,
    nome VARCHAR(80),
    classe_produto CHAR(1)
);

-- Tabela pedidos
CREATE TABLE pedidos (
    id_pedido INTEGER PRIMARY KEY,
    id_comanda INTEGER,
    id_cardapio INTEGER,
    qtde TINYINT
);

-- Tabela cardapio_itens
CREATE TABLE cardapio_itens (
    cardapio_itens INT PRIMARY KEY,
    nome VARCHAR(80),
    qtde TINYINT,
    id_cardapio INTEGER
);

-- Tabela funcionario
CREATE TABLE funcionario (
    id_funcionario INTEGER PRIMARY KEY,
    nome_funcionario VARCHAR(50),
    cargo VARCHAR(50),
    salario NUMERIC
);

-- Tabela pagamento
CREATE TABLE pagamento (
    id_pagamento INTEGER PRIMARY KEY,
    id_comanda INT,
    valor_pago NUMERIC,
    data_pagamento DATETIME
);

-- Adicionando chaves estrangeiras na tabela comanda
ALTER TABLE comanda
ADD CONSTRAINT fk_comanda_mesa FOREIGN KEY (id_mesa) REFERENCES mesa (id_mesa);

ALTER TABLE comanda
ADD CONSTRAINT fk_comanda_cliente FOREIGN KEY (id_cliente) REFERENCES cliente (id_cliente);

ALTER TABLE comanda
ADD CONSTRAINT fk_comanda_pedido FOREIGN KEY (id_pedido) REFERENCES pedidos (id_pedido);

-- Adicionando chaves estrangeiras na tabela pedidos
ALTER TABLE pedidos
ADD CONSTRAINT fk_pedidos_comanda FOREIGN KEY (id_comanda) REFERENCES comanda (id_comanda);

ALTER TABLE pedidos
ADD CONSTRAINT fk_pedidos_cardapio FOREIGN KEY (id_cardapio) REFERENCES cardapio (id_cardapio);

-- Adicionando chave estrangeira na tabela cardapio_itens
ALTER TABLE cardapio_itens
ADD CONSTRAINT fk_cardapio_itens_cardapio FOREIGN KEY (id_cardapio) REFERENCES cardapio (id_cardapio);

-- Adicionando chave estrangeira na tabela pagamento
ALTER TABLE pagamento
ADD CONSTRAINT fk_pagamento_comanda FOREIGN KEY (id_comanda) REFERENCES comanda (id_comanda);

