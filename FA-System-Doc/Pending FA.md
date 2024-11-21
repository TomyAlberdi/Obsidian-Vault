- [ ] Implementar estilos de carga en botones de formularios (Disabled until request is fullfiled).
	- [x] Category
	- [x] Subcategory
	- [x] Provider
	- [ ] Add Product
	- [ ] Update Product

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
			- [x] admin Stock
			- [ ] Download product detail
	- [ ] Complementary Info
		- [ ] Prettify Price
			- [ ] Add button to quick price & discount update
				- [ ] Implement patch price & discount in backend
		- [ ] Characteristics
			- [ ] Add tags for extra characteristics

- [ ] Implementar barras de búsqueda (Products, Categories, Providers)

- [ ] Crear página lista completa de Product Stock
	- [x] Crear página de registros completos de product stock
	- [ ] Implementar barra de búsqueda (Por Product name && Product ID)

- [ ] Add product characteristics + create & update methods (**Tags field ??**)
	- [ ] Create tags object (ex: {name: "color", value: "rojo"})
	- [ ] Add to product:
		- [ ] Color
		- [ ] Aspecto
		- [ ] Borde
		- [ ] Origen
		- [ ] Textura
		- [ ] Tránsito

- [ ] Implementar add product form functionality
	- [ ] Crear S3 Bucket + Configurar
	- [ ] Conectar frontend + backend para frontend image upload
		- [ ] Crear página de image upload and listing (Delete option) (Consultar Santiago)