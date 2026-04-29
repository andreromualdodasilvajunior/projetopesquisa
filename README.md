# Projeto de pesquisa geral - 2 DS (feito por: André Romualdo Da Silva Junior).
|Explicação do que é o padrão DAO e exemplo.|


-: O DAO (Data Access Object) é um padrão de projeto que encapsula o acesso aos dados em uma camada separada, permitindo que a lógica de negócios não tenha conhecimento direto das operações de acesso aos dados. Isso significa que a lógica do negócio permanece agnóstica em relação ao tipo de banco de dados. Ele surgiu com a necessidade de separarmos a lógica de negócios da lógica de persistência de dados. Este padrão permite que possamos mudar a forma de persistência sem que isso influencie em nada na lógica de negócio, além de tornar nossas classes mais legíveis.

Fontes: 

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

: Um detalhe técnico que o artigo deixa claro é o uso de interfaces para definir os métodos de acesso aos dados (CRUD) assim permitindo que diferentes implementações por exemplo, usando JDBC ou outro tipo de persistência possam ser trocadas sem atrapalhar o restante da aplicação.

Como usar no projeto)

: Usamos criando interfaces DAO para definir o CRUD e implementações separadas em dao.impl entao permitindo trocar a tecnologia de persistência sem alterar o restante do sistema.

exemplo:

import java.util.List;

public interface IProdutoDAO {
    void inserir(Produto p);
    List<Produto> listarTodos();
    void atualizar(Produto p);
    void deletar(int id);
}

