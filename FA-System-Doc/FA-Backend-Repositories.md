## Product:
### `ProductRepository`:
#### Product Utils:
- `updateById(String name, String description, Long categoryId, Long providerId, Integer discount_percentage, Double discount_new_price, String measures, Double m2PerBox, String priceUnit, String salesUnit, Double price, String quality, Long id)`
#### Image Utils:
- `deleteImagesById(Long id)`
- `insertImageById(String image, Long id)`
#### Tag Utils:
- `deleteTagsById(Long id)`
- `insertTagById(String tag, Long id)`
#### Filter Utils:
- `getMeasures()`
- `getPrices()`
#### Category Utils:
- `getIdByCategory(Long categoryId)`
- `getProductAmountByCategory(Long categoryId)`
- `getPartialProductStockByCategory(Long categoryId)`
#### Provider Utils:
- `getIdByProvider(Long providerId)`
- `getProductAmountByProvider(Long providerId)`
- `getPartialProductStockByProvider(Long providerId)`
### `ProductPaginatedRepository`:
-  `getPartialProducts(Pageable pageable)`
-  `getPartialProductsByKeyword(@Param("keyword") String keyword, Pageable pageable)`
## Category:
### `CategoryRepository`:
-  `findByName(String name)`
## Provider:
### `ProviderRepository`:
-  `findByName(String name)`
## Stock:
### `StockRepository`:
- `findByProductId(Long productId)`
- `getQuantityByProductId(Long productId)`
- `deleteByProductId(Long productId)`