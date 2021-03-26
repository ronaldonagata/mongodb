### Usar index para consumir menos memória e diminuir tempo de pesquisa
- https://docs.mongodb.com/manual/tutorial/sort-results-with-indexes/

### Alguns exemplos de queries no java
- https://www.devglan.com/spring-boot/spring-data-mongodb-queries

### Criar paginação com os dados de pageable a partir de uma lista
- https://www.baeldung.com/spring-thymeleaf-pagination

<code>
int pageSize = pageable.getPageSize();
int currentPage = pageable.getPageNumber();
int startItem = currentPage * pageSize;
List<Book> list;
if (books.size() < startItem) {
            list = Collections.emptyList();
} else {
int toIndex = Math.min(startItem + pageSize, books.size());
list = books.subList(startItem, toIndex);
}
Page<Book> bookPage = new PageImpl<Book>(list, PageRequest.of(currentPage, pageSize), books.size());
</code>
