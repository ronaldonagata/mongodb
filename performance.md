Recurso que utiliza muita memória:
* Aggregation
* Index Traversing
* Write Operations
* Query Engine
* Connections

Mongo vai tentar usar todos os cores da cpu:
* Page Compression
* Data Calculation
* Aggregation Framework Operations
* Map Reduce

Obs: Operações que podem ser bloqueantes update no mesmo documento... é bloqueante logo , multiples threads não vai ajudar.

O storeEngine default usado pelo mongo é o WiredTiger, ele se beneficia de multiplas request de escrita e leitura utilizado os cores das cpus, quando é feito em registros diferentes

O mongo se beneficia do raid 10

Index -> ajuda a resolver slow queries.

Collection scan -> O(n) ---> procurar em todos os documentos
Usa B-tree para guardar as chaves dos indíces
Index Overhead -> demora pra inserir, deletar p um documento novo pois tem que varrer as b-trees

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
    * Quando existem múltiplos predicados, os predicados que possuem os indexes são utilizados primeiros e os sem indexes são utilizados depois,,, assim otimizando.
  
    


