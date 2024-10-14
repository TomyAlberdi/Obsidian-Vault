## Generic return functions:
### `notFound(String dataType, String data)`:
```java
public ResponseEntity<?> notFound(String dataType, String data) {  
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Category with " + dataType + " " + data + " not found");  
}
```
### `existingAttribute(String dataType, String data)`:
```java
public ResponseEntity<?> existingAttribute(String dataType, String data) {  
    return ResponseEntity.status(HttpStatus.BAD_REQUEST).body("Category with " + dataType + " " + data + " already exists");  
}
```
## Category:
### `CategoryController`:
#### `list()`:
```java
@GetMapping()  
public ResponseEntity<?> list() {  
    return ResponseEntity.status(HttpStatus.OK).body(categoryService.list());  
}
```
#### `get(String identifier)`:
```java
@GetMapping("/{identifier}")  
public ResponseEntity<?> get(@PathVariable String identifier) {  
    try {  
        Long id = Long.parseLong(identifier);  
        Optional<Category> category = categoryService.findById(id);  
        return category.isEmpty()  
                ? notFound("ID", identifier)  
                : ResponseEntity.ok(category.get());  
    } catch (NumberFormatException e) {  
        Optional<Category> category = categoryService.findByName(identifier);  
        return category.isEmpty()  
                ? notFound("Name", identifier)  
                : ResponseEntity.ok(category.get());  
    }  
}
```
#### `save(String name)`:
```java
@PostMapping("/{name}")  
public ResponseEntity<?> save(@PathVariable String name) {  
    Optional<Category> repeatedCategory = categoryService.findByName(name);  
    if (repeatedCategory.isPresent()) {  
        return existingAttribute("Name", name);  
    }  
    Category newCategory = categoryService.save(name);  
    return ResponseEntity.status(HttpStatus.CREATED).body(newCategory);  
}
```
#### `delete(Long id)`:
```java
@DeleteMapping("/{id}")  
public ResponseEntity<?> delete(@PathVariable Long id) {  
    Optional<Category> category = categoryService.findById(id);  
    if (category.isPresent()) {  
        categoryService.deleteById(id);  
        return ResponseEntity.ok("Category with ID " + id + " deleted successfully");  
    }  
    return notFound("ID", Long.toString(id));  
}
```
## Provider:
### `ProviderController`:
#### `list()`:
```java
@GetMapping()  
public ResponseEntity<?> list() {  
    return ResponseEntity.status(HttpStatus.OK).body(providerService.list());  
}
```
#### `get(String identifier)`:
```java
@GetMapping("/{identifier}")  
public ResponseEntity<?> get(@PathVariable String identifier) {  
    try {  
        Long id = Long.parseLong(identifier);  
        Optional<Provider> provider = providerService.findById(id);  
        return provider.isEmpty()  
                ? notFound("ID", identifier)  
                : ResponseEntity.ok(provider.get());  
    } catch (NumberFormatException e) {  
        Optional<Provider> provider = providerService.findByName(identifier);  
        return provider.isEmpty()  
                ? notFound("Name", identifier)  
                : ResponseEntity.ok(provider.get());  
    }  
}
```
#### `save(String name)`:
```java
@PostMapping("/{name}")  
public ResponseEntity<?> save(@PathVariable String name) {  
    Optional<Provider> repeatedProvider = providerService.findByName(name); 
    if (repeatedProvider.isPresent()) {  
        return existingAttribute("Name", name);  
    }  
    Provider newProvider = providerService.save(name);  
    return ResponseEntity.status(HttpStatus.CREATED).body(newProvider);  
}
```
#### `delete(Long id)`:
```java
@DeleteMapping("/{id}")  
public ResponseEntity<?> delete(@PathVariable Long id) {  
    Optional<Provider> provider = providerService.findById(id);  
    if (provider.isPresent()) {  
        providerService.deleteById(id);  
        return ResponseEntity.ok("Provider with ID " + id + " deleted successfully");  
    }  
    return notFound("ID", Long.toString(id));  
}
```
## Product:
### `ProductController`:
#### `list(int page, int size)`:
```java
@GetMapping()  
public ResponseEntity<Page<PartialProductDTO>> list(  
        @RequestParam(value = "page", defaultValue = "0") int page,  
        @RequestParam(value = "size", defaultValue = "9") int size) {  
    return ResponseEntity.ok(productService.getPaginatedPartialProducts(page, size));  
}
```
#### `searchProductByKeyword(int page, int size)`:
```java
@GetMapping("/filterList")  
public ResponseEntity<Page<PartialProductDTO>> getPartialProducts(  
        FilterDTO filterDTO,  
        @RequestParam(value = "page", defaultValue = "0") int page,  
        @RequestParam(value = "size", defaultValue = "9") int size) {  
    return ResponseEntity.ok(productService.getFilteredPartialProducts(filterDTO, page, size));  
}
```
#### `getById(Long id)`:
```java
@GetMapping("/{id}")  
public ResponseEntity<?> getById(@PathVariable Long id) {  
    Optional<CompleteProductDTO> product = productService.getById(id);  
    return product.isPresent()  
            ? notFound("ID", id.toString())  
            : ResponseEntity.ok(product);  
}
```
#### `getMeasures()`:
```java
@GetMapping("/measures")  
public ResponseEntity<?> getMeasures() {  
    return ResponseEntity.ok(productService.getMeasure());  
}
```
#### `getPrices()`:
```java
@GetMapping("/prices")  
public ResponseEntity<?> getPrices() {  
    return ResponseEntity.ok(productService.getPrices());  
}
```
#### `addList(List<Product> products)`:
```java
@PostMapping("/addList")  
// @PreAuthorize("hasAuthority('ROLE_admin')")  
public ResponseEntity<?> addList(@Valid @RequestBody List<Product> products) {  
    for (Product product : products) {  
        if (productService.searchKeys(product.getCategoryId(), product.getProviderId())) {  
            productService.add(product);  
        }  
    }  
    return ResponseEntity.status(HttpStatus.CREATED).body("Products with existing providers and categories created.");  
}
```
#### `deleteById(Long id)`:
```java
@DeleteMapping("/{id}")  
// @PreAuthorize("hasAuthority('ROLE_admin')")  
public ResponseEntity<?> deleteById(@PathVariable Long id) {  
    Optional<CompleteProductDTO> product = productService.getById(id);  
    if (product.isPresent()) {  
        productService.deleteById(id);  
        return ResponseEntity.ok("Product with id " + id + " deleted.");  
    }  
    return notFound("ID", id.toString());  
}
```
#### `updateById(Product product)`:
```java
@PutMapping()  
// @PreAuthorize("hasAuthority('ROLE_admin')")  
public ResponseEntity<?> updateById(@Valid @RequestBody Product product) {  
    Optional<CompleteProductDTO> newProduct = productService.getById(product.getId());  
    if (newProduct.isEmpty()) {  
        return notFound("ID", product.getId().toString());  
    }  
    Optional<Category> category = categoryService.findById(product.getCategoryId());  
    Optional<Provider> provider = providerService.findById(product.getProviderId());  
    if (category.isEmpty()) {  
        return notFound("Category ID", product.getCategoryId().toString());  
    }  
    if (provider.isEmpty()) {  
        return notFound("Provider ID", product.getProviderId().toString());  
    }  
    productService.updateProduct(product);  
    return ResponseEntity.ok("Product updated.");  
}
```