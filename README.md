# db_aula_16_05
Exercicio finalizado 

create database dbBANCO; 
use dbBANCO;  

create table tbcliente(
cpf bigint primary key,
nome varchar(50) not null,
sexo char(1) not null,
endereco varchar (50) not null,
E_mail varchar(100)
);
create table tbconta(
numeroConta int primary key,
saldo decimal (7,2),
TipoConta smallint, 
NumeroAgencia int not null,
foreign key (NumeroAgencia) references tbagencia(NumeroAgencia)
);
alter table tbconta add NumeroAgencia int not null;
alter table tbconta add foreign key (NumeroAgencia) references tbagencia(NumeroAgencia);

create table tbbanco(
Codigo int primary key,
nome varchar(50)
);

create table tbtelefone_cliente(
cpf bigint,
foreign key (cpf) references tbcliente(cpf),
telefone int primary key
);

create table tbhistorico(
cpf bigint,
numeroConta int,
foreign key (cpf) references tbcliente(cpf),
foreign key (numeroConta) references tbconta(numeroConta),
DataInicio date,
primary key(cpf, numeroConta)
);

create table tbagencia(
Codigo int null, 
foreign key(Codigo) references tbbanco(Codigo),
NumeroAgencia int primary key,
endereco varchar(50)
); 

insert into tbbanco(codigo, nome)
values ('1', 'Banco do Brasil'),
('104', 'Caixa Econômica Federal'),
('801', 'Banco Escola');

insert into tbagencia(Codigo, NumeroAgencia, endereco)
values ('1', '123', 'Av Paulista, 78'),
('104', '159', 'Rua Liberdade, 124'),
('801', '401', 'Rua Vinte três. 23'),
('801', '435', 'Av Marechal, 68');

insert into tbcliente(cpf, nome, sexo, endereco)
values('12345678910', 'Enildo', 'M', 'Rua Grande, 75'),
('12345678911', 'Astrogildo', 'M', 'Rua Pequena, 789'),
('12345678912', 'Monica', 'F', 'Av Larga, 148'),
('12345678913', 'Cascâo', 'M', 'Av Principal, 369');

insert into tbconta(numeroConta, saldo, TipoConta, NumeroAgencia)
values('9876', '456.05','1', '123'),
('9877', '321.00', '1', '123'),
('9878', '100.00', '2', '435'),
('9879', '5589.89', '1', '401');

insert into tbhistorico(cpf, numeroconta, datainicio)
values('12345678910', '9876', '2001-04-15'),
('12345678911', '9877', '2011-03-10'),
('12345678912', '9878', '2021-03-11'),
('12345678913', '9879', '2000-07-05');

insert into tbtelefone_cliente(cpf, telefone)
values('12345678910', '912345678'),
('12345678911', '912345679'),
('12345678912', '912345680'),
('12345678913', '912345681');
alter table tbconta drop column NumAgencia;
describe tbconta;

alter table tbcliente add e_mail varchar(100);
select * from tbcliente where nome = 'Monica'; 
select cpf, endereco from tbcliente where nome = 'Monica';
select numeroagencia, endereco from tbagencia where numeroagencia  159 ;                           
select * from tbcliente where sexo = 'M'; 

select numeroagencia, endereco from tbagencia;


-- ex 1 

delete from tbtelefone_cliente where telefone = '912345679';  
select * from tbtelefone_cliente;


-- ex 2(parte 2)
update tbConta set tipoConta = 2 where NumeroConta = 9879;
select * from tbconta;


-- ex 3 (parte2)

insert into tbcliente(e_mail)
values('Astro@Escola.com');

update tbcliente set e_mail = 'Astro@Escola.com' where nome = 'Monica';

select * from tbcliente;

SET SQL_SAFE_UPDATES = 0;

-- ex 4

update tbConta set tipoConta = 1 where NumeroConta = 9876; 
update tbConta set saldo = Saldo + Saldo * 10/100 where NumeroConta = 9876; 
select * from tbConta;

-- fechado 

-- ex5
select nome, e_mail, endereco from tbcliente where nome = 'Monica';

-- fechado 

-- ex 6

update tbcliente set nome = 'Enildo Candito' where nome = 'Enildo'; 
update tbcliente set e_mail = 'enildo@escola.com' where nome = 'Enildo Candito';

select * from tbcliente where nome = 'Enildo Candito';
select * from tbcliente; 

-- fechado

-- ex7 

update tbconta set saldo =  Saldo-30;
select * from tbConta;

-- fechado 

-- ex8

delete from tbconta where numeroConta = '9878';
select * from tbconta;

-- Não é possivel deletar, pois ela deve existir, pois a chave estrangeira garante a sua integridade. Sua exclusão pode ser realizada porém gerará diversos problemas.

-- fechado


describe 
select * from tbbanco;
select * from tbagencia;
