## Entities:
##### `Category`:
```java
public class Category {  
    @Id  
    @GeneratedValue(strategy = GenerationType.AUTO)  
    private Long id;  
      
    @NotBlank  
    @Column(unique = true)  
    private String name;  
      
    @Column(name = "products_amount")  
    private Integer productsAmount = 0;   
}
```
##### `Provider`:
```java
public class Provider {  
    @Id  
    @GeneratedValue(strategy = GenerationType.AUTO)  
    private Long id;  
      
    @NotBlank  
    @Column(unique = true)  
    private String name;  
      
    @Column(name = "products_amount")  
    private int productsAmount = 0;       
}
```
##### `Product`:
```java
public class Product {  
    @Id  
    @GeneratedValue(strategy = GenerationType.AUTO)  
    private Long id;  
      
    @Column(name = "provider_id")  
    @NotBlank  
    private Long providerId;  
      
    @NotBlank  
    @Column(name = "category_id")  
    private Long categoryId;  
      
    @NotNull  
    @ElementCollection    @CollectionTable(name = "product_tags", joinColumns = @JoinColumn(name = "product_id"))  
    @Column  
    private List<String> tags;  
      
    @NotNull  
    @ElementCollection    @CollectionTable(name = "product_images", joinColumns = @JoinColumn(name = "product_id"))  
    @Column  
    private List<String> images;  
      
    @NotBlank  
    @Column(unique = true)  
    private String name;  
      
    @NotNull  
    @Column    private String description;  
      
    @NotBlank  
    @Column    private Double price;  
      
    @Column  
    @NotNull    // 13cm x 13cm  
    private String measures;  
      
    @NotNull  
    @Column(name = "sale_unit")  
    // M2  
    private String saleUnit;  
      
    @NotNull  
    @Column(name = "price_sale_unit")  
    // 100$ x M2  
    private Double priceSaleUnit;  
      
    @NotNull  
    @Column(name = "unit_per_box")  
    // 10 M2 per box  
    private Double unitPerBox;  
      
    @NotNull  
    @Column    private String quality;  
      
    @NotNull  
    @Column(name = "discount_percentage")  
    private Integer discountPercentage;  
      
    @NotNull  
    @Column(name = "discounted_price")  
    private Double discountedPrice;  
}
```
## DTOs:
##### `CategoryDTO`:
```java
public class CategoryDTO {  
    private String name;   
}
```
##### `ProviderDTO`:
```java
public class ProviderDTO {  
    private String name;       
}
```
##### `CompleteProductDTO`:
```java
public class CompleteProductDTO {  
    private Long id;  
    private String name;  
    private String description;  
    private Double price;  
    private String measures;  
    private String saleUnit;  
    private Double priceSaleUnit;  
    private Double unitPerBox;  
    private String quality;  
    private Integer discountPercentage;  
    private Double discountedPrice;  
      
    private List<String> tags;  
    private List<String> images;  
      
    private String category;  
    private String provider;       
}
```
##### `PartialProductDTO`:
```java
public class PartialProductDTO {  
    private Long id;  
    private String name;  
    private Double price;  
    private String salesUnit;  
    private Double priceSaleUnit;  
    private Integer discountPercentage;  
    private Double discountedPrice;  
      
    private String image;       
}
```
##### `FilterDTO`:
```java
public class FilterDTO {  
    private Long categoryId;  
    private Long providerId;  
    private String measure;  
    private Double minPrice;  
    private Double maxPrice;  
    private Boolean discount;  
}
```
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