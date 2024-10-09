## Product:
### `ProductRepository`:
Used to return complete, non-paginated lists of Products, individual fields, counts or characteristics
##### `getIdByCategory(Long id)`:
```sql
SELECT p.id FROM Product p WHERE p.categoryId = ?1
```
Returns all the **ids** of products with a specific category. Used in the [[FA-Backend-Controllers#`CategoryController`|Category Controller]] to verify if any Products have a specific category before deleting it.
##### `getProductAmountByCategory(Long id)`:
```sql
SELECT COUNT(p) AS amount FROM Product p WHERE p.categoryId = ?1
```
Returns a count of all the products that a specific category has. Used to display this count in [[FA-Frontend|Frontend]] Product filters.
##### `getIdByProvider(Long id)`:
```sql
SELECT p.id FROM Product p WHERE p.providerId = ?1
```
Ídem first method but for providers.
##### `getProductAmountByProvider(Long id)`:
```sql
SELECT COUNT(p) AS amount FROM Product p WHERE p.providerId = ?1
```
Ídem second method but for providers.
##### `getMeasures()`:
```sql
SELECT new MeasureDTO(p.measures, COUNT(p)) FROM Product p GROUP BY p.measures ORDER BY COUNT(p) DESC
```
Generates a [[FA-Backend-Entities#`MeasureDTO`|MeasureDTO]] for each Product measure. Used to display a list of methods and the amount of products they contain in the Frontend Product filters.
##### `getPrices()`:
```sql
SELECT new PricesDTO(MIN(p.price), MAX(p.price)) FROM Product p
```
Returns a [[FA-Backend-Entities#`PricesDTO`|PricesDTO]] to display in the Frontend Product filters.
##### `updateById(String name, String description, Long categoryId, Long providerId, Integer discount_percentage, Double discount_new_price, String measures, Double m2PerBox, String priceUnit, String salesUnit, Double price, String quality, Long id)`:
```sql
UPDATE Product SET name = ?1, description = ?2, categoryId = ?3, providerId = ?4, discountPercentage = ?5, discountedPrice = ?6, measures = ?7, unitPerBox = ?8, priceSaleUnit = ?9, saleUnit = ?10, price = ?11, quality = ?12 WHERE id = ?13
```
Updates a product by ID.
##### `deleteImagesById(Long code)`:
```sql
DELETE FROM product_images WHERE product_id = ?1
```
Deletes all the images associated with a specific product.
##### `insertImageById(String image, Long id)`:
```sql
INSERT INTO product_images (product_id, images) VALUES (?2, ?1)
```
Insert an image URL into a specific product.
##### `deleteTagsById(Long code)`:
```sql
DELETE FROM product_tags WHERE product_id = ?1
```
Deletes all the tags associated with a specific product.
##### `insertTagById(String tag, Long id)`:
```sql
INSERT INTO product_tags (product_id, tags) VALUES (?2, ?1)
```
Insert a tag into a specific product.
### `ProductPaginatedRepository`:
##### `getPartialProducts(Pageable pageable)`:
```sql
SELECT new PartialProductDTO(p.id, p.name, p.price, p.saleUnit, p.priceSaleUnit, p.discountPercentage, p.discountedPrice, '') FROM Product p
```
Returns a page of reduced data Products for Frontend card displaying.
##### `getPartialProductsByKeyword(@Param("keyword") String keyword, Pageable pageable)`:
```sql
SELECT PartialProductDTO(p.id, p.name, p.price, p.saleUnit, p.priceSaleUnit, p.discountPercentage, p.discountedPrice, '') FROM Product p LEFT JOIN Category c ON p.categoryId = c.id LEFT JOIN Provider pr ON p.providerId = pr.id WHERE LOWER(p.name) LIKE LOWER(CONCAT('%', :keyword, '%')) OR LOWER(p.description) LIKE LOWER(CONCAT('%', :keyword, '%')) OR LOWER(c.name) LIKE LOWER(CONCAT('%', :keyword, '%')) OR LOWER(pr.name) LIKE LOWER(CONCAT('%', :keyword, '%')) OR :keyword MEMBER OF p.tags
```
Returns a page of filtered reduced data Products for Frontend filtered cards displaying.
## Category:
## Provider: