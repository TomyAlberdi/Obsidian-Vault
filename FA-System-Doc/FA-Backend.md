## EML v0.1
![[Pasted image 20241008154850.png]]
## Product
### Entities:
#### [[FA-Backend-Entities#Product|ProductEntity]]
#### [[FA-Backend-Entities#CompleteProductDTO|CompleteProductDTO]]
#### [[FA-Backend-Entities#PartialProductDTO|PartialProductDTO]]
### Repositories:
#### [[FA-Backend-Repositories#`ProductRepository`|ProductRepository]]
#### [[FA-Backend-Repositories#`ProductPaginatedRepository`|ProductPaginationRepository]]
### Services:
#### [[FA-Backend-Services#`ProductService`|ProductService]]
### Controller:
#### [[FA-Backend-Controllers#`ProductController`|ProductController]]

## Category
### Entities:
#### [[FA-Backend-Entities#`Category`|CategoryEntity]]
#### [[FA-Backend-Entities#`CategoryDTO`|CategoryDTO]]
### Repositories:
#### [[FA-Backend-Repositories#`CategoryRepository`|CategoryRepository]]
### Services:
#### [[FA-Backend-Services#`CategoryService`|CategoryService]]
### Controller:
#### [[FA-Backend-Controllers#`CategoryController`|CategoryController]]
## Provider
### Entities:
#### [[FA-Backend-Entities#`Provider`|ProviderEntity]]
#### [[FA-Backend-Entities#`ProviderDTO`|ProviderDTO]]
### Repositories:
#### [[FA-Backend-Repositories#`ProviderRepository`|ProviderRepository]]
### Services:
#### [[FA-Backend-Services#`ProviderService`|ProviderService]]
### Controller:
#### [[FA-Backend-Controllers#`ProviderController`|ProviderController]]
## Filter
### Entities:
#### [[FA-Backend-Entities#`FilterDTO`|FilterDTO]]
#### [[FA-Backend-Entities#`MeasureDTO`|MeasureDTO]]
#### [[FA-Backend-Entities#`PricesDTO`|PricesDTO]]
## Hooks:
### [[FA-Backend-Hooks#`ProductSpecifications`|ProductSpecifications]]
## [[FA-Database|Database]] connection:
```properties
# Spring Datasource Config  
spring.datasource.url=jdbc:mysql://localhost:3333/FA-db  
spring.datasource.username=root  
spring.datasource.password=root  
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver  
  
# Hibernate Config  
spring.jpa.hibernate.ddl-auto=update  
spring.jpa.show-sql=false
```