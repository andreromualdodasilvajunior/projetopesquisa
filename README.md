# Projeto de pesquisa geral - 2 DS (feito por: André Romualdo Da Silva Junior).

# |Explicação do que é o padrão DAO e exemplos.|


-: O DAO (Data Access Object) é um padrão de projeto que encapsula o acesso aos dados em uma camada separada, permitindo que a lógica de negócios não tenha conhecimento direto das operações de acesso aos dados. Isso significa que a lógica do negócio permanece agnóstica em relação ao tipo de banco de dados. Ele surgiu com a necessidade de separarmos a lógica de negócios da lógica de persistência de dados. Este padrão permite que possamos mudar a forma de persistência sem que isso influencie em nada na lógica de negócio, além de tornar nossas classes mais legíveis.

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



# Fontes: 

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


