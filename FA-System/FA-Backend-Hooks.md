## `ProductSpecifications`:
#### `hasCategory(Long categoryId)`:
```java
public static Specification<Product> hasCategory(Long categoryId) {  
    return (root, query, builder) -> categoryId == null ? builder.conjunction() : builder.equal(root.get("categoryId"), categoryId);  
}
```
#### `hasProvider(Long providerId)`:
```java
public static Specification<Product> hasProvider(Long providerId) {  
    return (root, query, builder) -> providerId == null ? builder.conjunction() : builder.equal(root.get("providerId"), providerId);  
}
```
#### `hasMeasure(String measure)`:
```java
public static Specification<Product> hasMeasure(String measure) {  
    return (root, query, builder) -> measure == null ? builder.conjunction() : builder.equal(root.get("measures"), measure);  
}
```
#### `priceBetween(Double minPrice, Double maxPrice)`
```java
public static Specification<Product> priceBetween(Double minPrice, Double maxPrice) {  
    return (root, query, builder) -> {  
        if (minPrice == null && maxPrice == null) {  
            return builder.conjunction();  
        } else if (minPrice != null && maxPrice != null) {  
            return builder.between(root.get("price"), minPrice, maxPrice);  
        } else if (minPrice != null) {  
            return builder.greaterThanOrEqualTo(root.get("price"), minPrice);  
        } else {  
            return builder.lessThanOrEqualTo(root.get("price"), maxPrice);  
        }  
    };  
}
```
#### `hasDiscount(Boolean discount)`:
```java
public static Specification<Product> hasDiscount(Boolean discount) {  
    return (root, query, builder) -> {  
        if (discount == null) {  
            return builder.conjunction();  
        } else if (discount) {  
            return builder.isNotNull(root.get("discountPercentage"));  
        } else {  
            return builder.isNull(root.get("discountPercentage"));  
        }  
    };  
}
```