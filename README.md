
# Projeto Integrador (Grupo 13) - Senac

2º Entrega:

Desenvolvimento do sistema de cadastro universitário 🏫

O sistema deve contemplar o cadastro de pessoas físicas e jurídicas, alunos, 
fornecedores e professores, cada um com seus próprios requisitos e necessidade de 
acesso as informações da universidade.

## Requisitos 

### Geral
- [x] Página inicial
- [x] Página contato
- [x] Tela do administrador
- [x] Exclusão de conta
  
### Professor 👩‍🔬
- [x] 🔹 Portal do professor
- [x] 🔹 Lista de disciplinas/turmas

### Aluno 🧑‍🎓
- [x] 🔹 Portal do aluno 
- [x] 🔹 Matrícula em disciplinas
  
### Fornecedor 👨‍💼
- [x] 🔹 Portal do fornecedor 🏭
- [x] 🔹 Cadastro de produtos
- [x] 🔹 Atualização de estoque e valores dos produtos

---
## Prototipação

### Geral
#### Página inicial
![Página inicial](documentacao/prototipos/prototipo-pagina-inicial.png)

#### Página de contato
![Página de contato](documentacao/prototipos/prototipo-fale-conosco.jpg)

#### Página de exclusão de conta
![Exclusão de conta](documentacao/prototipos/prototipo-exclusao.jpg)

---
### Portal do professor
![Portal do professor](documentacao/prototipos/prototipo-portal-do-professor.jpg)

---

### Portal do Aluno
![Portal do aluno](documentacao/prototipos/prototipo-portal-do-aluno.jpg)

---
### Portal do Fornecedor
![Portal do fornecedor](documentacao/prototipos/prototipo-portal-do-fornecedor.jpg)
---
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
    Aluno <|-- Disciplina

    Fornecedor --|> Produto
    
    class Pessoa {
        - Id: int
        - Matricula: string
        - Nome: string
        - Endereco: string
        - Email: string
        - Telefone: string
        - Ativo: bool
        - Admin: bool
        + cadastrar() void
        + validaAdmin() bool
        + atualizar() void
    }
    class PessoaJuridica {
        - Pessoa: Pessoa
        - CNPJ: string
        - RazaoSocial: string
        - NomeFantasia: string
        - InscricaoEstadual: string
        + cadastrar()
        + atualizar()
    }
    class PessoaFisica {
        - Pessoa: Pessoa
        - CPF: string
        + cadastrar()
        + atualizar()
    }
    class Professor {
        - PessoaFisica: PessoaFisica
        - PessoaJuridica: PessoaJuridica
        - Disciplinas: [Disciplina]
        + calcularSalario() decimal
        + listarDisciplinas() [Disciplina]
    }
    class Aluno {
        - PessoaFisica: PessoaFisica
        - Curso: string
        - Disciplinas: [Disciplina]
        - DataInicio: datetime
        + consultarNota() void
        + acessarBoleto() void
        + consultarDisciplinas() void
        + listarDisciplinas() [Disciplina]
    }
    class Disciplina {
        - Id: int
        - Nome: string
        - cargaHoraria: decimal
        - Professor: Professor
        - Alunos: [Aluno]
        + defineProfessor(Professor) void
        + matriculaAluno(Aluno) void
        + listarAlunos() [Aluno]
    }
    class Fornecedor {
        - PessoaJuridica: PessoaJuridica
        - Produtos: [Produto]
        + solicitarNotaFiscal() void
        + consultarEstoque() void
    }
    class Produto {
        - Id: int
        - Nome: string
        - Valor: decimal
        - Estoque: decimal
        + alterarEstoque(qtd) void
        + alterarValor(valor) void
    }
```

## Diagrama de caso de uso
![Diagrama de caso de uso](documentacao/diagramas/diagrama_de_caso_de_uso.png "Diagrama de caso de uso")
