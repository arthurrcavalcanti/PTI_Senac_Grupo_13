# PTI_Senac_Grupo_13
2º entrega do Projeto Integrador

## Requisitos
Aluno:
- Cadastro de conta com informações pesoais
- Exclusão de conta
- Matrícula em disciplinas
  
Professor:
- Cadastro de conta com informações pessoais
- Caso exista adicionar informações de pessoa jurídica
- Adicionar professor a uma disciplina
- Consultar salário

Fornecedor:
- Cadastro de conta com informações da empresa
- Cadastro de pessoa Jurídica
- Cadastro de produtos
- Cadastro de estoque dos produtos
   

## Diagramas / UML

```mermaid
---
title: Diagrama de classes
---
classDiagram
    Pessoa <|-- PessoaJuridica
    Pessoa <|-- PessoaFisica

    PessoaJuridica <|-- Professor
    PessoaJuridica <|-- Fornecedor
    PessoaFisica <|-- Professor
    PessoaFisica <|-- Aluno

    Professor --|> Disciplina
    Professor <-- Disciplina
    Aluno --|> Disciplina

    Fornecedor --|> Produto
    
    class Pessoa {
        - Id: int
        - Nome: string
        - Endereco: string
        - Email: string
        - Telefone: string
        - Ativo: bool
        - Admin: bool
        + Cadastrar() Pessoa
        + Validar() bool
        + Alterar() bool
    }
    class PessoaJuridica {
        - Pessoa: Pessoa
        - CNPJ: string
        - RazaoSocial: string
        - NomeFantasia: string
        - InscricaoEstadual: string
    }
    class PessoaFisica {
        - Pessoa: Pessoa
        - CPF: string
    }
    class Professor {
        - PessoaFisica: PessoaFisica
        - PessoaJuridica: PessoaJuridica
        - Matricula: string
        - Disciplinas: [Disciplina]
        + calcularSalario() decimal
    }
    class Aluno {
        - PessoaFisica: PessoaFisica
        - Matricula: string
        - Curso: string
        - Disciplinas: [Disciplina]
        - DataInicio: datetime
        + consultarNota() void
        + acessarBoleto() void
        + consultarDisciplinas() void
    }
    class Disciplina {
        - Id: int
        - Nome: string
        - cargaHoraria: decimal
        - Professor: Professor
        - Alunos: [Aluno]
        + matriculaAluno(Aluno) void
    }
    class Fornecedor {
        - PessoaJuridica: PessoaJuridica
        - Produtos: [Produto]
        - Quantidade: decimal
        + solicitarNotaFiscal() void
        + consultarEstoque() void
    }
    class Produto {
        - Id: int
        - Nome: string
        - Valor: decimal
    }
```