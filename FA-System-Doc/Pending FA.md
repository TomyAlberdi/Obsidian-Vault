- Añadir nuevos campos a proveedor: Localidad, dirección, teléfono, email y CUIT.
	- [x] Aplicar cambios en entity, DTO, repository, service, controller y relaciones con otros componentes.
	- [x] Actualizar formulario web de creación de proveedores.
	- [x] Actualizar página de proveedor con nuevos campos.
	- [ ] (Posible) Agregar filtros de búsqueda de proveedores.

- Modificar sistema de categorías:
	- [x] Agregar subcategorías.
	- [x] Modificar página de categoría con lista de subcategorías.
	- [ ] (Posible) Agregar filtros de búsqueda de categorías y subcategorías.

- [x] Category, Subcategory & Provider *product lists*
	- [x] Fix Price
		- [x] Normalize `saleUnitPrice = measurePrice` in cases where `saleUnitType !== M2, ML, CM2`.
	- [x] Fix Price unit (Currently only M2)

- [x] Implementar subcategory page
	- [x] Subcategory administration
	- [x] Add subcategory form from Category page

- [ ] Implementar estilos de carga en botones de formularios (Disabled until request is fullfiled).
	- [x] Category
	- [x] Subcategory
	- [x] Provider
	- [ ] Product

- [ ] Display discounted price in category, subcategory, provider product lists.
	- [ ] Add to DTO
	- [ ] Modify Services.

- [ ] Implementar product page
	- [x] Add product link on product card and product lists click.
	- [x] Image Carousel
	- [x] Main Info
	- [ ] Administration Panel
		- [x] Button Visual
		- [ ] Button Functionality
			- [ ] Edit product. Create page + implement form (Possibly reuse Create Product page)
			- [ ] Delete Product
			- [ ] Disable/Enable Product
			- [ ] Update Stock
			- [ ] Download product detail
	- [ ] Complementary Info
		- [ ] Prettify Price
		- [x] Stock & Last 5 records
		- [ ] Characteristics
			- [ ] Add tags for extra characteristics

- [ ] Creat página lista completa de Product Stock

- [ ] Add product characteristics + create & update methods (**Tags field ??**)
	- [ ] Create tags object (ex: {name: "color", value: "rojo"})
	- [ ] Add to product:
		- [ ] Color
		- [ ] Aspecto
		- [ ] Borde
		- [ ] Origen
		- [ ] Textura
		- [ ] Tránsito

- [x] (Backend) Implement product disabled/discontinued boolean field + corresponding methods.
	- [x] Add filter by discontinued product.

- [x] Implementar product list filter functionality
	- [x] (Posible) Implementar filtro por subcategory

- [ ] Implementar add product form functionality
	- [ ] Crear S3 Bucket + Configurar
	- [ ] Conectar frontend + backend para frontend image upload
		- [ ] Crear página de image upload and listing (Delete option) (Consultar Santiago)