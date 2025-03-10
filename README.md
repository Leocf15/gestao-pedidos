# Gestão de Pedidos - Oracle PL/SQL

Este projeto é um exemplo prático de um sistema de **Gestão de Pedidos** utilizando **PL/SQL, Triggers, Views e Procedures** no **Oracle Database**.

## 📌 Tecnologias Utilizadas
- **Oracle Database**
- **PL/SQL**
- **Triggers e Views**
- **Procedures**

## 📂 Estrutura do Projeto
- **Tabelas**: CLIENTES e PEDIDOS
- **Procedures**: Inserção de pedidos
- **Triggers**: Atualização automática do status do pedido
- **Views**: Lista de pedidos aprovados

## 🚀 Como Executar o Projeto
1. **Clone o repositório**
   ```sh
   git clone https://github.com/seuusuario/gestao-pedidos-oracle.git
   cd gestao-pedidos-oracle
   ```
2. **Conecte-se ao Oracle Database** usando uma ferramenta como SQL*Plus ou SQL Developer.
3. **Execute os scripts SQL** na ordem correta para criar as tabelas e objetos do banco.

## 📜 Estrutura do Banco de Dados
### **Tabela CLIENTES**
```sql
CREATE TABLE CLIENTES (
    ID_CLIENTE NUMBER PRIMARY KEY,
    NOME VARCHAR2(100) NOT NULL,
    EMAIL VARCHAR2(100) UNIQUE
);
```
### **Tabela PEDIDOS**
```sql
CREATE TABLE PEDIDOS (
    ID_PEDIDO NUMBER PRIMARY KEY,
    ID_CLIENTE NUMBER,
    DATA_PEDIDO DATE DEFAULT SYSDATE,
    TOTAL NUMBER(10,2),
    STATUS VARCHAR2(20) DEFAULT 'PENDENTE',
    CONSTRAINT FK_PEDIDO_CLIENTE FOREIGN KEY (ID_CLIENTE) REFERENCES CLIENTES(ID_CLIENTE)
);
```
### **Procedure de Inserção de Pedido**
```sql
CREATE OR REPLACE PROCEDURE INSERIR_PEDIDO(
    p_id_pedido NUMBER,
    p_id_cliente NUMBER,
    p_total NUMBER
) AS
BEGIN
    INSERT INTO PEDIDOS (ID_PEDIDO, ID_CLIENTE, TOTAL)
    VALUES (p_id_pedido, p_id_cliente, p_total);
    COMMIT;
END;
/
```
### **Trigger para Atualização do Status do Pedido**
```sql
CREATE OR REPLACE TRIGGER TRG_ATUALIZAR_STATUS
BEFORE UPDATE ON PEDIDOS
FOR EACH ROW
BEGIN
    IF :NEW.TOTAL > 1000 THEN
        :NEW.STATUS := 'APROVADO';
    ELSE
        :NEW.STATUS := 'PENDENTE';
    END IF;
END;
/
```
### **View de Pedidos Aprovados**
```sql
CREATE OR REPLACE VIEW VW_PEDIDOS_APROVADOS AS
SELECT * FROM PEDIDOS WHERE STATUS = 'APROVADO';
```

## 📌 Próximos Passos
- Implementar **Oracle Forms** para entrada de dados
- Criar relatórios em **Oracle Reports**
- Melhorar regras de negócios no PL/SQL

## 📄 Licença
Este projeto é de código aberto e pode ser utilizado para estudos e melhorias. 🚀
