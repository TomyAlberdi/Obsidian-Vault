## Category:
### `CategoryController`:
- `list()`
- `get(String identifier)`
- `save(String name)`
- `delete(Long id)`
- `forceDelete(Long id)`
## Provider:
### `ProviderController`:
- `list()`
- `get(String identifier)`
- `save(String name)`
- `delete(Long id)`
- `forceDelete(Long id)`
## Product:
### `ProductController`:
- `list(int page, int size)`
- `searchProductByKeyword(int page, int size)`
- `getById(Long id)`
- `getFilteredPartialProducts(FilterDTO filter, int page, int size)`
- `save(Product product)`
- `deleteById(Long id)`
- `updateById(Product product)`
- `getPartialByCategory(Long categoryId)`
- `getPartialByProvider(Long providerId)`
## Filter:
### `FilterController`:
- `getMeasures()`
- `getPrices()`
## Stock:
### `StockController`:
- `list()`
- `increaseStock(@RequestParam Long productId, @RequestParam Integer quantity)`
- `reduceStock(@RequestParam Long productId, @RequestParam Integer quantity)`