## Product:
### `ProductService`:
#### Basic CRUD:
- `add(Product product)`
- `getById(Long id)`
- `updateProduct(Product product)`
- `deleteById(Long id)`
#### Pagination & Filter Utils:
- `getPaginatedPartialProducts(int page, int size)`
- `getFilteredPartialProducts(FilterDTO filterDTO, int page, int size)`
- `searchProductsByKeyword(String keyword, int page, int size)`
#### Category Utils:
- `getIdByCategory(Long categoryId)`
- `getPartialProductStockByCategory(Long categoryId)`
- `deleteProductByCategoryId(Long categoryId)`
#### Provider Utils:
- `getIdByProvider(Long providerId)`
- `getPartialProductStockByProvider(Long providerId)`
- `deleteProductByProviderId(Long providerId)`
#### Image and Tag Utils:
- `getProductTags(Long productId)`
- `getProductImages(Long productId)`
#### Other Utils:
- `searchKeys(Long categoryId, Long providerId)`
- `existByName(String name)`
- `existById(Long id)`
## Category:
### `CategoryService`:
- `list()`
- `findById(Long id)`
- `findByName(String name)`
- `getIdByCategory(Long categoryId)`
- `save(String name)`
- `deleteById(Long id)`
## Provider:
### `ProviderService`:
- `list()`
- `findById(Long id)`
- `findByName(String name)`
- `getIdByProvider(Long providerId)`
- `save(String name)`
- `deleteById(Long id)`
## Filter:
### `FilterService`:
- `getMeasure()`
- `getPrices()`
## Stock:
### `StockService`:
- `findAll()`
- `getByProductId(Long productId)`
- `save(Long productId, String productName)`
- `increaseStockById(Long productId, Integer quantity)`
- `decreaseStockById(Long productId, Integer quantity)`
- `deleteStockByProductId(Long productId)`
- `addStockRecordToStock(Stock stock, StockRecord record)`