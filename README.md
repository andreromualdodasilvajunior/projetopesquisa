# Projeto de pesquisa geral - 2 DS (feito por: André Romualdo Da Silva Junior).

# |Explicação do que é o padrão DAO e exemplos.|


-: O DAO (Data Access Object) é um padrão de projeto que encapsula o acesso aos dados em uma camada separada, permitindo que a lógica de negócios não tenha conhecimento direto das operações de acesso aos dados. Isso pelo que observei significa que a lógica do negócio permanece agnóstica em relação ao tipo de banco de dados, esse padrão permite que possamos mudar a forma de persistência sem que isso influencie em nada na lógica de negócio, além de tornar nossas classes mais legíveis.

# |O que ele evita?|

-: o DAO evita o SQL espalhado pelo código, reduzindo o acoplamento e facilitando a manutenção, a organização e a troca de banco de dados.

# |O que vai em cada camada?|


# model (objetos)

São classes que representam as entidades do sistema, contendo atributos e getters/setters.

# dao (interfaces/contratos)

 Define os métodos de acesso aos dados (CRUD) e não o possui código SQL.

# dao.impl (implementação)

implementa as interfaces DAO e clntém SQL e uso de JDBC (PreparedStatement, ResultSet).

# db (conexão e exceções)

o ConnectionFactory, cria conexões com o banco.

já o DbException, trata e padroniza erros do banco.

# app (menu e orquestração)

Classe principal (Main), interação com o usuário e chama os métodos dos DAOs (sem o SQL direto).



# |fontes|: 

1- https://www.devmedia.com.br/dao-pattern-persistencia-de-dados-utilizando-o-padrao-dao/30999

Ideia principal do artigo) 

: Aprendermos como desenvolver um controle de acesso e cadastro de usuários orientado a objetos, separando o sistema em três camadas lógicas, a camada de lógica de negócios, a camada de acesso a dados e a camada de visualização, utilizando o padrão DAO, O padrão organiza as operações CRUD e promove a independência de tecnologia.

Detalhe tecnico)

:  Um detalhe tecnico que observei durante a pesquisa foi que no Artigo diz que se aplicarmos este padrão (DAO) corretamente ele vai abstrair completamente o modo de busca e gravação dos dados, tornando isso transparente para aplicação e facilitando muito na hora de fazermos manutenção na aplicação ou de migrarmos de um banco de dados.


Como usar no projeto)

: Organizando o projeto em camadas (app, lógica e DAO), centralizando o CRUD nos DAOs e abstraindo o acesso ao banco com interfaces e implementações.



2-
https://medium.com/@felipe.damasceno.b/padr%C3%B5es-de-projeto-e-o-data-access-object-dao-7d7e4818866c

Ideia principal do artigo)

: Explicar o padrão de projeto DAO como uma forma de separar a lógica de acesso a dados da lógica de negócio.

Detalhe técnico)

: Um detalhe técnico que o artigo deixa claro e podemos observar é o uso de interfaces para definir os métodos de acesso aos dados (CRUD) assim permitindo que diferentes implementações por exemplo, usando JDBC ou outro tipo de persistência possam ser trocadas sem atrapalhar o restante da aplicação.

Como usar no projeto)

: Usamos criando interfaces DAO para definir o CRUD e implementações separadas em dao.impl entao permitindo trocar a tecnologia de persistência sem alterar o restante do sistema.


3- https://www.dio.me/articles/o-que-e-dao-ba9c73921265

Ideia principal do artigo)

: Explicar o padrão DAO como uma forma de separar a lógica de acesso a dados da lógica de negócio, reduzindo o acoplamento além de que melhorando a organização do sistema fica mais fácil de aplicarmos no projeto.

Detalhe técnico)

: Um detalhe técnico observado é que antes do uso do DAO o código SQL ficava espalhado meio confuso pela aplicação e o padrão resolve isso centralizando todas as operações de acesso aos dados em um único lugar pra ficar menos desorganizado.

Como usar no projeto)

: usamos quando concentrando todo acesso ao banco nas classes DAO, evitando SQL no Main e deixando o código mais organizado e fácil de modificar.


4- https://blog.singularityubrazil.com/blog/dao/

Ideia principal do artigo)

: Apresentar o conceito de DAO no nosso contexto geral assim mostrando a ideia de organização baseada em regras bem definidas e separação de setores e responsabilidade.

Detalhe técnico)

: Um detalhe técnico que observei é que o conceito trabalha com regras fáceis e não complicadas e estrutura organizada, onde cada parte do sistema tem sua função específica então evitando mistura de responsabilidades e conceitos.

Como usar no projeto)

: Aplicamos criando DAOs com funções bem definidas como o CRUD, mantendo cada parte do sistema organizada e com responsabilidade única sem embaralhar suas funções.


5- https://www.macoratti.net/11/10/pp_dao1.htm

Ideia principal do artigo)

: Mostrar que o padrão DAO resolve problemas como código repetido, difícil manutenção e forte acoplamento e que ele separa o acesso aos dados da lógica da aplicação.

Detalhe técnico)

: Um detalhe técnico importante é que todo acesso ao banco deve passar pelo DAO, que encapsula as operações CRUD e permite trocar a fonte de dados sem afetar o restante do sistema.

Como usar no projeto)

: Aplicamos garantindo que todo acesso ao banco fique dentro de dao.impl usando interfaces DAO e mantendo o restante do sistema independente do banco.




exemplos:

1-
import java.util.List;

public interface IProdutoDAO {
    void inserir(Produto p);
    List<Produto> listarTodos();
    void atualizar(Produto p);
    void deletar(int id);
}


2-
class LivroDAO:
    def __init__(self):
        self.banco_dados = []

    def salvar(self, livro):
        self.banco_dados.append(livro)
        print(f"Livro '{livro.titulo}' salvo com sucesso")

    def listar(self):
        return self.banco_dados

    def buscar_por_id(self, id):
        for livro in self.banco_dados:
            if livro.id == id:
                return livro
        return None



# |Ciclo de vida da conexão JDBC|

-: Basicamente o ciclo de vida da conexão JDBC representa todas as etapas desde a abertura da conexão até o fechamento dos recursos após executar operações no banco de dados e ela compreende a sequência padronizada de operações para estabelecer, utilizar e encerrar a comunicação entre uma aplicação Java e um banco de dados relacional até por que este ciclo garante o gerenciamento adequado de recursos.


# |Etapas|

1:
# Carregar configurações
ler db.properties (URL, usuário, senha)

2:
# Abrir conexão
criar conexão com o banco usando DriverManager.getConnection entre outros.

3:
# Preparar o SQL
criar um PreparedStatement com a query usando ?.

4:
# Definir parâmetros
passar valores com setString, setInt, etc.

5:
# Executar comando
executeQuery() (SELECT)
executeUpdate() (INSERT, UPDATE, DELETE)

6:
# Processar resultado
ler dados com ResultSet e transformar em objetos (model)

7:
# Fechar recursos
fechar ResultSet, PreparedStatement e Connection, preferencialmente com try-with-resources.



# DriverManager.getConnection(...)

O DriverManager é a classe responsável por gerenciar uma lista de drivers JDBC registrados e estabelecer conexões físicas com o banco de dados, a partir da URL,o usuário e a senha definidos no db.properties, sendo o ponto inicial de qualquer operação com o JDBC


# PreparedStatement

O PreparedStatement é uma interface que representa uma instrução SQL pré-compilada que permite a vinculação segura de parâmetros em tempo de execução.


# executeUpdate() vs executeQuery()

Ambos são métodos de Statement e PreparedStatement, mas possuem finalidades e retornos diferentes.

executeUpdate() é utilizado para comandos que alteram dados (como INSERT, UPDATE, DELETE), retornando a quantidade de linhas afetadas, enquanto executeQuery() é usado para SELECT, retornando um ResultSet com os dados da consulta.


# ResultSet 

O ResultSet armazena os dados retornados do banco e permite percorrer os resultados, sendo utilizado para converter cada registro em objetos Java (model) exemplo: em um método instantiateX(rs).

# |fontes|

1- https://www.dio.me/articles/jdbc-java-database-connectivity-uma-visao-geral-57b6b447ec8d

Ideia principal do artigo)

: Explicar o funcionamento do JDBC como uma API que permite a comunicação entre aplicações Java e bancos de dados.

Detalhe técnico)

: Um detalhe técnico lá é que o JDBC segue um fluxo de etapas bem definidas, como abrir conexão, facilitando a organização no acesso.

Como usar no projeto)

: Aplicamos seguindo esse fluxo dentro dos DAOs, garantindo que toda operação com o banco siga uma sequência mais organizada.


2- https://www.devmedia.com.br/jdbc-alem-do-basico/32338

Ideia principal do artigo)

: Mostrar o uso do JDBC de forma mais aprofundada, como diz no título além do basico destacando boas práticas no uso de conexões e comandos SQL.

Detalhe técnico)

: Um detalhe técnico no geral é o uso correto de PreparedStatement e o gerenciamento de recursos para evitar problemas como vazamento de conexão.

Como usar no projeto)

: Aplicamos utilizando PreparedStatement e garantindo o fechamento correto das conexões dentro do DAO em nosso projeto.


3-
 https://www.servicenow.com/docs/r/pt-BR/xanadu/servicenow-platform/orchestration/t_CreateAJDBCActivity.html

Ideia principal do artigo)

: a ideia é explicar como funciona a integração com banco de dados utilizando JDBC em atividades automatizadas.

Detalhe técnico)

: E um detalhe técnico observado é a necessidade de configurar corretamente a conexão e os parâmetros antes de executar qualquer operação lá no banco de dados.

Como usar no projeto)

: usamos no projeto quando garantindo que a conexão seja sempre configurada corretamente através do ConnectionFactory antes de executar qualquer SQL.


4- https://www.ibm.com/docs/pt-br/was-nd/8.5.5?topic=architecture-connection-life-cycle

Ideia principal do artigo)

: a ideia é basicamente apresentar o ciclo de vida da conexão com banco de dados, mostrando os estados que uma conexão pode ter durante seu uso.

Detalhe técnico)

: Um detalhe técnico importante é que a conexão pode estar em estados como: em uso, sendo gerenciada conforme a aplicação que precisa utilizar ou liberar recursos. 

Como usar no projeto)

: Aplicamos basicamente quando a gente abre conexões apenas quando necessário e fechando certinho após o uso, evitando desperdício de recursos pra não bagunçar e fica até confuso pra achar onde usamos algo que pode dar erro.

5- https://pt.linkedin.com/pulse/understanding-basics-jdbc-java-database-connectivity-animireddy-6ynnc?tl=pt

Ideia principal do artigo)

: Explicar os conceitos básicos do JDBC e como ele permite executar comandos SQL e manipular dados em aplicações Java.

Detalhe técnico)

: e um detalhe técnico é que o JDBC segue etapas como criar conexão, preparar comandos, executar queries e processar resultados antes de finalizar a conexão. 


como usar no projeto)

: basicamente aplicamos seguindo esse ciclo dentro dos métodos DAO, garantindo que cada operação no banco siga todas as etapas.

# |Segurança (SQL Injection e PreparedStatement)|

SQL Injection

-: SQL Injection é uma falha de segurança que ocorre quando comandos SQL são montados por meio de concatenação de strings, permitindo que usuários malvados ou hackers insiram códigos SQL dentro de campos de entrada e alterem o comportamento da consulta.

PreparedStatement

-: O PreparedStatement evita SQL Injection pois separa o comando SQL dos dados, utilizando parâmetros (?) que são tratados de forma segura pelo banco de dados.


exemplo:

String sql = "SELECT * FROM usuario WHERE nome = ?";
PreparedStatement ps = conn.prepareStatement(sql);
ps.setString(1, nome);

# Transações

-: Transações são um conjunto de operações realizadas no banco de dados que devem ser executadas completamente ou não serem executar desse jeito garantindo a integridade dos dados.


# |meu Mapa Conceitual|

DAO 
│
-Interface (dao/)
│   define contrato CRUD: inserir(),   buscarPorId(), atualizar(), deletar()
│
-Implementação (dao.impl/)
│  - Usa JDBC: Connection, PreparedStatement, ResultSet
│  -SQL centralizado e parametrizado (?)
│  -mapeamento ResultSet = Model via instantiateX(rs)
│

JDBC
- ConnectionFactory (db/)
│  - Lê db.properties
│  - retorna Connection via DriverManager.getConnection()
│
- PreparedStatement
│  - Previne SQL Injection
│  - permite reutilização de plano de execução
│
- executeQuery() = ResultSet (SELECT)
- executeUpdate() = int (INSERT/UPDATE/DELETE)
│

Exceções
 SQLException (checked) = encapsulada em DbException (runtime)
- mensagens padronizadas para diagnóstico
│

Transações 
- begin -  operações múltiplas - commit / rollback
= bem util quando várias tabelas são afetadas atomicamente
