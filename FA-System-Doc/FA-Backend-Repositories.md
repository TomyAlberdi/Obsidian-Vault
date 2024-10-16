## Product:
### `ProductRepository`:
##### `getIdByCategory(Long id)`:
```sql
SELECT p.id FROM Product p WHERE p.categoryId = ?1
```
##### `getProductAmountByCategory(Long id)`:
```sql
SELECT COUNT(p) AS amount FROM Product p WHERE p.categoryId = ?1
```
##### `getIdByProvider(Long id)`:
```sql
SELECT p.id FROM Product p WHERE p.providerId = ?1
```
##### `getProductAmountByProvider(Long id)`:
```sql
SELECT COUNT(p) AS amount FROM Product p WHERE p.providerId = ?1
```
##### `getMeasures()`:
```sql
SELECT new MeasureDTO(p.measures, COUNT(p)) FROM Product p GROUP BY p.measures ORDER BY COUNT(p) DESC
```
##### `getPrices()`:
```sql
SELECT new PricesDTO(MIN(p.price), MAX(p.price)) FROM Product p
```
##### `updateById(String name, String description, Long categoryId, Long providerId, Integer discount_percentage, Double discount_new_price, String measures, Double m2PerBox, String priceUnit, String salesUnit, Double price, String quality, Long id)`:
```sql
UPDATE Product SET name = ?1, description = ?2, categoryId = ?3, providerId = ?4, discountPercentage = ?5, discountedPrice = ?6, measures = ?7, unitPerBox = ?8, priceSaleUnit = ?9, saleUnit = ?10, price = ?11, quality = ?12 WHERE id = ?13
```
##### `deleteImagesById(Long code)`:
```sql
DELETE FROM product_images WHERE product_id = ?1
```
##### `insertImageById(String image, Long id)`:
```sql
INSERT INTO product_images (product_id, images) VALUES (?2, ?1)
```
##### `deleteTagsById(Long code)`:
```sql
DELETE FROM product_tags WHERE product_id = ?1
```
##### `insertTagById(String tag, Long id)`:
```sql
INSERT INTO product_tags (product_id, tags) VALUES (?2, ?1)
```
### `ProductPaginatedRepository`:
```java
public interface ProductPaginationRepository extends PagingAndSortingRepository<Product, Long>, JpaSpecificationExecutor<Product>
```
##### `getPartialProducts(Pageable pageable)`:
```sql
SELECT new PartialProductDTO(p.id, p.name, p.price, p.saleUnit, p.priceSaleUnit, p.discountPercentage, p.discountedPrice, '') FROM Product p
```
##### `getPartialProductsByKeyword(@Param("keyword") String keyword, Pageable pageable)`:
```sql
SELECT PartialProductDTO(p.id, p.name, p.price, p.saleUnit, p.priceSaleUnit, p.discountPercentage, p.discountedPrice, '') FROM Product p LEFT JOIN Category c ON p.categoryId = c.id LEFT JOIN Provider pr ON p.providerId = pr.id WHERE LOWER(p.name) LIKE LOWER(CONCAT('%', :keyword, '%')) OR LOWER(p.description) LIKE LOWER(CONCAT('%', :keyword, '%')) OR LOWER(c.name) LIKE LOWER(CONCAT('%', :keyword, '%')) OR LOWER(pr.name) LIKE LOWER(CONCAT('%', :keyword, '%')) OR :keyword MEMBER OF p.tags
```
## Category:
### `CategoryRepository`:
##### `findByName(String name)`:
```sql
SELECT c FROM Category c WHERE c.name = ?1
```
## Provider:
### `ProviderRepository`:
##### `findByName(String name)`:
```sql
SELECT p FROM Provider p WHERE p.name = ?1
```