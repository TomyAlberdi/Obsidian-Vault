## Product:
### `ProductService`:
#### `searchKeys(Long categoryId, Long providerId)`:
```java
public Boolean searchKeys(Long categoryId, Long providerId) {  
    Optional<Category> category = categoryRepository.findById(categoryId);  
    Optional<Provider> provider = providerRepository.findById(providerId);  
    return category.isPresent() && provider.isPresent();  
}
```
#### `getPaginatedPartialProducts(int page, int size)`:
```java
public Page<PartialProductDTO> getPaginatedPartialProducts(int page, int size) {  
    Pageable pageable = PageRequest.of(page, size);  
    Page<PartialProductDTO> partialProductDTOPage = productPaginationRepository.getPartialProducts(pageable);  
      
    List<PartialProductDTO> PartialProductDTOList = partialProductDTOPage.getContent().stream().toList();  
      
    for (PartialProductDTO PartialProductDTO : PartialProductDTOList) {  
        Optional<List<String>> images = this.getProductImages(PartialProductDTO.getId());  
        images.ifPresent(strings -> PartialProductDTO.setImage(strings.get(0)));  
    }  
    return new PageImpl<>(PartialProductDTOList, pageable, partialProductDTOPage.getTotalElements());  
}
```
#### `getFilteredPartialProducts(FilterDTO filterDTO, int page, int size)`:
```java
public Page<PartialProductDTO> getFilteredPartialProducts(FilterDTO filterDTO, int page, int size) {  
    Pageable pageable = PageRequest.of(page, size);  
      
    Specification<Product> spec = Specification.where(ProductSpecifications.hasCategory(filterDTO.getCategoryId()))  
            .and(ProductSpecifications.hasProvider(filterDTO.getProviderId()))  
            .and(ProductSpecifications.hasMeasure(filterDTO.getMeasure()))  
            .and(ProductSpecifications.priceBetween(filterDTO.getMinPrice(), filterDTO.getMaxPrice()))  
            .and(ProductSpecifications.hasDiscount(filterDTO.getDiscount()));  
      
    return productPaginationRepository.findAll(spec, pageable).map(product ->  
            new PartialProductDTO(product.getId(), product.getName(), product.getPrice(), product.getSaleUnit(), product.getPriceSaleUnit(), product.getDiscountPercentage(), product.getDiscountedPrice(), product.getImages().get(0))  
    );  
}
```
#### `searchProductsByKeyword(String keyword, int page, int size)`:
```java
public Page<PartialProductDTO> searchProductsByKeyword(String keyword, int page, int size) {  
    Pageable pageable = PageRequest.of(page, size);  
    Page<PartialProductDTO> partialProductDTOPage = productPaginationRepository.getPartialProductsByKeyword(keyword, pageable);  
    List<PartialProductDTO> PartialProductDTOList = partialProductDTOPage.getContent().stream().toList();  
    return new PageImpl<>(PartialProductDTOList, pageable, partialProductDTOPage.getTotalElements());  
}
```
#### `add(Product product)`:
```java
public Product add(Product product) {  
    return productRepository.save(product);  
}
```
#### `getById(Long id)`:
```java
public Optional<CompleteProductDTO> getById(Long id) {  
    Optional<Product> product = productRepository.findById(id);  
    return Optional.of(convertDTO(product.get()));  
}
```
#### `getIdByCategory(Long categoryId)`:
```java
public Optional<List<Long>> getIdByCategory(Long categoryId) {  
    return productRepository.getIdByCategory(categoryId);  
}
```
#### `getIdByProvider(Long providerId)`:
```java
public Optional<List<Long>> getIdByProvider(Long providerId) {  
    return productRepository.getIdByProvider(providerId);  
}
```
#### `deleteById(Long id)`:
```java
public void deleteById(Long id) {  
    productRepository.deleteById(id);  
}
```
#### `updateProduct(Product product)`:
```java
public void updateProduct(Product product) {  
    productRepository.deleteImagesById(product.getId());  
    productRepository.deleteTagsById(product.getId());  
    productRepository.updateById(product.getName(), product.getDescription(), product.getCategoryId(), product.getProviderId(), product.getDiscountPercentage(), product.getDiscountedPrice(), product.getMeasures(), product.getUnitPerBox(), product.getPriceSaleUnit(), product.getSaleUnit(), product.getPrice(), product.getQuality(), product.getId());  
    for (String tag : product.getTags()) {  
        productRepository.insertTagById(tag, product.getId());  
    }  
    for (String image : product.getImages()) {  
        productRepository.insertImageById(image, product.getId());  
    }  
}
```
#### `getProductTags(Long productId)`:
```java
public Optional<List<String>> getProductTags(Long productId) {  
    return productRepository.findById(productId).map(Product::getTags);  
}
```
#### `getProductImages(Long productId)`:
```java
public Optional<List<String>> getProductImages(Long productId) {  
    return productRepository.findById(productId).map(Product::getImages);  
}
```
#### `getMeasure()`:
```java
public List<MeasureDTO> getMeasure() {  
    return productRepository.getMeasures();  
}
```
#### `getPrices()`:
```java
public PricesDTO getPrices() {  
    return productRepository.getPrices();  
}
```
## Category:
### `CategoryService`:
#### `list()`:
```java
public List<Category> list() {  
    return categoryRepository.findAll();  
}
```
#### `findById(Long id)`:
```java
public Optional<Category> findById(Long id) {  
    return categoryRepository.findById(id);  
}
```
#### `findByName(String name)`:
```java
public Optional<Category> findByName(String name) {  
    return categoryRepository.findByName(name);  
}
```
#### `save(String name)`:
```java
public Category save(String name) {  
    Category newCategory = new Category();  
    newCategory.setName(name);  
    return categoryRepository.save(newCategory);  
}
```
#### `deleteById(Long id)`:
```java
public void deleteById(Long id) {  
    categoryRepository.deleteById(id);  
}
```
## Provider:
### `ProviderService`:
#### `list()`:
```java
public List<Provider> list() {  
    return providerRepository.findAll();  
}
```
#### `findById(Long id)`:
```java
public Optional<Provider> findById(Long id) {  
    return providerRepository.findById(id);  
}
```
#### `findByName(String name)`:
```java
public Optional<Provider> findByName(String name) {  
    return providerRepository.findByName(name);  
}
```
#### `save(String name)`:
```java
public Provider save(String name) {  
    Provider newProvider = new Provider();  
    newProvider.setName(name);  
    return providerRepository.save(newProvider);  
}
```
#### `deleteById(Long id)`:
```java
public void deleteById(Long id) {  
    providerRepository.deleteById(id);  
}
```