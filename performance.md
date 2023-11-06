Recurso que utiliza muita memória:
* Aggregation
* Index Traversing
* Write Operations
* Query Engine - to retrieve query results
* Connections

Mongo ill try to use all the cpu ores by default:
* Page Compression
* Data Calculation
* Aggregation Framework Operations
* Map Reduce

OBS: Operations that works at the same document can be blocking, like update operations, so multiples threads and cpus won't help to achieve better performance,

Obs: Operações que podem ser bloqueantes update no mesmo documento... é bloqueante logo , multiples threads não vai ajudar.

O storeEngine default usado pelo mongo é o WiredTiger, ele se beneficia de multiplas request de escrita e leitura utilizado os cores das cpus, quando é feito em registros diferentes

O mongo se beneficia do raid 10

Index -> ajuda a resolver slow queries.

* Collection scan -> O(n) ---> procurar em todos os documentos.
* Mongo usa B-tree para guardar as chaves dos indíces, a complexida é log(n) pois depende da altura da árvore.
* Index Overhead -> cuidado ao criar muitos indices, pois pode demorar pra inserir, deletar p um documento novo pois tem que varrer as b-trees.

Como os dados são guardados no disco --> WiredTiger Engine
* Cada collection ou índice é criado um arquivo .wt
* Setar uma pasta para as collections e index, e colocar um link simbólico para discos diferentes, pode otimizar a leitura e a escrita.
* db.collection.insert({...}, {writeConcern: {w:3}}) , db.collection.insert({...}, {writeConcern: {w:1, j:true}}) -> faz com que o que esteja na memoria ram seja persistido no disco ... ele não espera pelo **checkpoint** passar.

*** Single Field Index
* db.<collection>.createIndex({<field>:<direction>})
  * Key Features
    * Chaves de um único campo .Ex: CPF
    * Pode pesquisar um único elemento do campo indexado.
    * Pode pesquisar um range de valores
    * db.examples.explain("executionStats").find({}) --> **IXSCAN** , **COLLSCAN**
    * Pode usar usar dot notation para indexar campos em subdocumentos.
    * Pode encontrar múltiplos valores distintos em uma única query. 
    * Quando existem múltiplos predicados, os predicados que possuem os indexes são utilizados primeiros e os sem indexes são utilizados depois,,, assim otimizando a busca.
 
*** Explain 
* exp = db.<collection>.explain() --> criar um objeto com o explain, ajuda a não precisar escrever explain em toda query
* exp = db.<collection>.explain("queryPlanner") --> é o mesmo que executar sem parâmetro, modo default é o queryplanner. **Não executa a query**
* exp = db.<collection>.explain("executionStats") -->  **Executa a query**
* exp = db.<collection>.explain("allPlansExecution") --> **Executa a query**
 
 
 
