- Añadir nuevos campos a proveedor: Localidad, dirección, teléfono, email y CUIT.
	- [x] Aplicar cambios en entity, DTO, repository, service, controller y relaciones con otros componentes.
	- [x] Actualizar formulario web de creación de proveedores.
	- [x] Actualizar página de proveedor con nuevos campos.
	- [ ] (Posible) Agregar filtros de búsqueda de proveedores.

- Modificar sistema de categorías:
	- [x] Agregar subcategorías.
	- [ ] (Posible) Agregar "Familia".
	- [x] Modificar página de categoría con lista de subcategorías.
	- [ ] (Posible) Agregar filtros de búsqueda de categorías y subcategorías.

- [x] Category, Subcategory & Provider *product lists*
	- [x] Fix Price
		- [x] Normalize `saleUnitPrice = measurePrice` in cases where `saleUnitType !== M2, ML, CM2`.
	- [x] Fix Price unit (Currently only M2)

- [ ] Implementar subcategory page
	- [x] Subcategory administration
	- [ ] Add subcategory Link from Category page

- [ ] Implementar product page
	- [ ] Add product link on product card click

- [x] Implementar product list filter functionality
	- [x] (Posible) Implementar filtro por subcategory

- [ ] Implementar add product form functionality
	- [ ] Crear S3 Bucket + Configurar
	- [ ] Conectar frontend + backend para frontend image upload
		- [ ] Crear página de image upload and listing (Delete option) (Consultar Santiago)