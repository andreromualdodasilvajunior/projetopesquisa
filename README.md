# Projeto de pesquisa geral - 2 DS (feito por: André Romualdo Da Silva Junior).
|Explicação do que é o padrão DAO e exemplo.|
-R:O DAO (Data Access Object) é um padrão de projeto que encapsula o acesso aos dados em uma camada separada, permitindo que a lógica de negócios não tenha conhecimento direto das operações de acesso aos dados. Isso significa que a lógica do negócio permanece agnóstica em relação ao tipo de banco de dados. Ele surgiu com a necessidade de separarmos a lógica de negócios da lógica de persistência de dados. Este padrão permite que possamos mudar a forma de persistência sem que isso influencie em nada na lógica de negócio, além de tornar nossas classes mais legíveis.

fontes: https://www.devmedia.com.br/dao-pattern-persistencia-de-dados-utilizando-o-padrao-dao/30999
https://medium.com/@felipe.damasceno.b/padr%C3%B5es-de-projeto-e-o-data-access-object-dao-7d7e4818866c

exemplo:
