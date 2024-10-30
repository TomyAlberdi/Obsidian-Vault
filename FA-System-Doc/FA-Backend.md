## EML v0.1
![[Pasted image 20241008154850.png]]
- [[FA-Backend-Entities]]
- [[FA-Backend-Repositories]]
- [[FA-Backend-Hooks]]
- [[FA-Backend-Services]]
- [[FA-Backend-Controllers]]
## [[FA-Database|Database]] Connection:
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
## Security Configuration:
```properties
## JWKS (JSON Web Key Set) URL for key retrieval  
kinde.jwks.url=https://fasa.kinde.com/.well-known/jwks  
  
## JWT issuer and audience (used in verification)  
kinde.issuer=https://fasa.kinde.com  
kinde.audience=fa-backend-api
```