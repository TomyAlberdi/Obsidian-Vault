## Entities:
##### `Category`:
Basic Category Entity.
```java
public class Category {  
    private Long id;  
    private String name;  
    private Integer productsAmount = 0;   
}
```
##### `Provider`:
Basic Provider Entity.
```java
public class Provider {  
    private Long id;  
    private String name;  
    private int productsAmount = 0;       
}
```
##### `Product`:
Basic Product Entity.
```java
public class Product {  
    private Long id;  
    private Long providerId;  
    private Long categoryId;  
    private List<String> tags;  
    private List<String> images;  
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
}
```
##### `Stock`:
Basic Stock Entity.
```java
public class Stock {  
    private Long id;  
    private Long productId;  
    private String productName;  
    private Integer quantity = 0;  
    private List<StockRecord> stockRecords;  
}
```
##### `StockRecord`:
Basic Record Entity of Stock changes:
```java
public class StockRecord {  
    private String recordType;  
    private Integer stockChange;  
    private LocalDateTime recordDate;  
}
```
## DTOs:
##### `CompleteProductDTO`:
Complete Product DTO, including Category and Provider names and Stock quantity.
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
	private Integer stock;    
}
```
##### `PartialProductDTO`:
Partial Product DTO with reduced data and only one image.
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
##### `PartialProductStockDTO`:
Partial Product DTO with reduced data and stock info for listing.
```java
public class PartialProductStockDTO {  
    private Long id;  
    private String name;  
    private Integer Stock;  
    private String saleUnit;  
    private Double price;   
}
```
##### `FilterDTO`:
Basic Filter DTO.
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
Basic Measure DTO.
```java
public class MeasureDTO {  
    private String measure;  
    private Long products;       
}
```
##### `PricesDTO`:
Basic Measure DTO.
```java
public class PricesDTO {  
    public Double minPrice;  
    public Double maxPrice;       
}
```
