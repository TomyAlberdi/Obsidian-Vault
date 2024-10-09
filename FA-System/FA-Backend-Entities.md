## Entities:
## DTOs:
##### `MeasureDTO`:
```java
public class MeasureDTO {  
    private String measure;  
    private Long products;       
}
```
Used to return a list of measures and the amount of products they contain.
##### `PricesDTO`:
```java
public class PricesDTO {  
    public Double minPrice;  
    public Double maxPrice;       
}
```
Used to return the minimum and maximum prices between all of the products.