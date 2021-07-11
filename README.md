# Francisco-1705126 Database
# 1- Descrição do Trabalho

Este trabalho, feito em conjunto com o Mateus Rocha, pretende demonstrar uma Base de Dados criada para um Centro de Testes de COVID-19, para a disciplina de Bases de Dados I do Instituto Politécnico da Guarda. Será apresentada a descrição da Base de Dados, as entidades, atributos e relacionamentos presentes no Modelo Entidade-Relacionamento, imagens dos modelos Lógico e Relacional, exemplos de uso da sintaxe dos comandos de SQL, e por fim uma conclusão.

# 2- Modelo E-R

Um modelo Entidade Relacionamento (ER) é um modelo de dados para descrever os dados ou aspetos de informação de um domínio de negócio ou seus requisitos de processo, de uma maneira abstrata que em última análise se presta a ser implementada em uma base de dados, como uma base de dados relacional. Os principais componentes dos Modelos Entidade-Relacionamento (ER) são as entidades (coisas, objetos) suas relações e armazenamento em bancos de dados.

## 2-1 Descrição da BD

É uma Base de Dados de um Centro de Testes de COVID-19, onde funcionários marcam testes para pacientes, enviam os dados dos testes realizados para laboratórios que, por fim, enviam o resultado do teste de volta.

BD: centro_testecovid

## 2-2 Entidades-tipo

Entidade é um grupo de coisas relevantes com propriedades semelhantes, que podem ser objetos reais ou imaginários, que são distintos de outros objetos (outras Entidades) e sobre o quais é
necessário guardar informação.

PACIENTE (IDPaciente, N_BilheteId, Nome, Genero, Data_Nascimento)

            PK * U    , *   , *   , o   , *        
FUNCIONÁRIO (IDFuncionario, N_BilheteId, Nome, Genero, Data_Nascimento, FUNCAO_Funcao_Id)

            PK U   ,   *   , *   , o   , *   , FK *      
FUNCAO (Funcao_Id, Actividade)

            PK  * U  ,    *
LABORATORIO (IDLab, Contribuinte,Nome,Telefone)

            PK U    , *   ,*   , o
       
TESTE (Teste_Id, Tipo_de_Teste,PACIENTE_Bilhete_Id, Hora)

            PK * U  , *  , * U FK,  *

## 2.3- Entidades-fracas

MORADA (Rua,Numero,Codigo_Postal,Cidade,Telemovel)
       O  ,*     ,*            ,*     , *
- entidade identificadora: FUNCIONARIO, PACIENTE

DADOS (Nome,Genero,Data_Nascimento)
       *  ,o  ,*
- entidade identificadora: FUNCIONARIO, PACIENTE

COMUNICACAO (Telemovel, EMail,Url_Webpage)
            *     U  , o U  , o U
- entidade identificadora: FUNCIONARIO, PACIENTE, LABORATORIO

DATAS (Timestamp, LABORATORIO_Contribuinte)
      *        , *                      
- entidade identificadora: FUNCIONARIO, PACIENTE, LABORATORIO

## 2.4- Atributos

Um atributo é um aspecto ou propriedade que descreve uma Entidade. Os Atributos irão representar as colunas das tabelas.

PACIENTE

IDPaciente: É o número único de cada paciente na base de dados.\
N_BilheteId: É o número do Bilhete de Identificação do paciente.


FUNCIONÁRIO

IDPaciente: É o número único de cada funcionário na base de dados.\
N_BilheteId: É o número do Bilhete de Identificação do funcionário.


FUNCAO

Funcao_Id: É o identificador numérico único de cada função dentro do laboratório de testes.\
Actividade: É a função propriamente dita de cada funcionário.


LABORATORIO

IDLab: É o número único de cada laboratório dentro da base de dados.\
Contribuinte: Número de contribuinte do laboratório.\
Nome: Nome do laboratório.\
Telefone: Contacto telefônico do laboratório.


TESTE

Teste_Id: É o identificado único de cada teste realizado, para casos em que o mesmo paciente tem mais de um teste.\
Tipo_de_Teste: Se o teste realizado foi RT-PCR, Antigeno, Rapido ou outro.\
Hora: A hora que o teste foi marcado para ser realizado.


MORADA

Rua: Endereço onde se situa o paciente ou funcionário.\
Numero: Número da residência.\
Codigo_Postal: Código postal da localidade.\
Cidade: A cidade atual.\
Telemovel: Meio de contacto do paciente ou funcionário.


DADOS

Nome: Nome completo do paciente ou funcionário.\
Genero: Gênero do paciente ou funcionário.\
Data_Nascimento: Data de nascimento do paciente ou funcionário.


COMUNICACAO

Telemovel: Meio de contacto do paciente, funcionário ou laboratório.\
EMail: Email do paciente, funcionário ou laboratório.\
Url_Webpage: Webpage do paciente, funcionário ou laboratório.


DATAS

Timestamp: Data do teste, marcação ou entrega de resultado.


## 2.5- Relações

Um Relacionamento é uma associação entre duas Entidades.

Pode ser de Um para Um – No Oracle, representa-se com uma linha simples em ambos os lados.
Um para Muitos / Muitos para Um – No Oracle, representa-se com pé de galinha no lado do Muitos.
Muitos para Muitos – No Oracle, representa-se com pé de galinha em ambos os lados.

REGISTAR_NOVO_PACIENTE (PACIENTE,MORADA,DADOS,COMUNICACAO)
- REGISTAR_PM (PACIENTE,MORADA) 1:M
- REGISTAR_PD (PACIENTE,DADOS) 1:M
- REGISTAR_PC (PACIENTE,COMUNICACAO) 1:M

REGISTAR_NOVO_FUNCIONARIO (FUNCIONARIO,MORADA,DADOS,COMUNICACAO)
- REGISTAR_FM (FUNCIONARIO,MORADA) 1:M
- REGISTAR_FD (FUNCIONARIO,DADOS)  1:M
- REGISTAR_FC (FUNCIONARIO,COMUNICACAO) 1:M

MARCARTESTE (TESTE,PACIENTE,FUNCIONARIO,LABORATORIO,DATAS)
- MARCARTESTE_PL (PACIENTE,TESTE_TesteId) N:M
- MARCARTESTE_FL (FUNCIONARIO,LABORATORIO) N:M
- MARCARTESTE_FD (FUNCIONARIO,PACIENTE_IDPaciente,DATAS) N:M
- MARCARTESTE_FD (FUNCIONARIO,LABORATORIO_IDLab,DATAS) N:M
- MARCARTESTE (TESTE,FUNCIONARIO_IDFuncionario,DATAS) N:M 

INFORMAR (FUNCIONARIO,PACIENTE,LABORATORIO,COMUNICACAO)
- INFORMA (FUNCIONARIO,PACIENTE) N:M
- INFORMA (FUNCIONARIO,LABORATORIO) N:M
- INFORMA (FUNCIONARIO,PACIENTE_IDPaciente,COMUNICACAO) N:M
- INFORMA (FUNCIONARIO,LABORATORIO_IDLab,COMUNICACAO) N:M

## 2.6- Modelo Lógico

O modelo lógico mostra as ligações entre as tabelas de bases de dados, as chaves primárias, os componentes de cada uma, etc.

![Aal text](imagens/covid1.PNG "Imagem")
## 2.7- Modelo Relacional

O modelo Relacional (ou Físico) é a instanciação do Modelo Lógico numa Base de Dados específica, seguindo as regras próprias dessa Base de Dados.

![Aal text](imagens/covid2.PNG "Imagem")

# 3- Exemplos de uso da syntax dos comandos SQL

## 3.1- Geral

## 3.2 SQL Server/Oracle/MS Access


## 3.3 MySQL

# 4- Conclusão

O projeto de criação desta Base de Dados foi desafiador pelo fato de ser o primeiro contato que tivemos com o software SQL Developer e com Bases de Dados prática - já havíamos estudado um pouco de teoria em Levantamentos de Requisitos.

O conhecimento de SQL Developer aumentou durante o semestre, embora até ao final, há certas opções e possibilidades quase "escondidas", e de difícil acesso, como para modificar as Foreign Keys que já haviam sido declaradas no início do semestre para melhorar o projeto agora ao final, já que temos mais entendimento de como as Bases de Dados funcionam no geral, e termos utilizado bastante na disciplina de Programação também.

Apesar das dificuldades e do tempo necessário para concretizar determinadas ações, a construção dos modelos ER, se bem planeadas anteriormente, é de fácil entendimento e feitura. Tivemos mais dificuldade para atualizar os dados feitos no início do semestre do que se criássemos todas as tabelas novamente, com as Entidades, Atributos e Relações completamente definidas.

Podemos concluir que atingimos o objetivo do trabalho, que era de criar uma Base de Dados funcional, com todo o Modelo ER configurado. Através dos modelos Lógico e Relacional, é possível partir para a criação das tabelas e de todo o sistema de base de dados de uma clínica de COVID-19 sem problemas, utilizando esta Base de Dados criada.


# 5- Bibliografia

(1) Modelo entidade relacionamento [Consult. 11 Julho 2021]. Disponível na WWW: URL: https://pt.wikipedia.org/wiki/Modelo_entidade_relacionamento.
