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

Obs: Operações que podem ser bloqueantes update no mesmo documento.. é bloqueante logo , multilples threads não vai ajudar.

O storeEngine default usado pelo mongo é o WiredTiger, ele se beneficia de multiplas request de escrita e leitura utilizado os cores das cpus, quando é feito em registros diferentes

O mongo se beneficia do raid 10


