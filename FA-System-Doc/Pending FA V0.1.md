- [ ] Implementar estilos de carga en botones de formularios (Disabled until request is fullfiled).
	- [x] Category
	- [x] Subcategory
	- [x] Provider
	- [ ] Add Product
	- [ ] Update Product

- [ ] Implementar product page
	- [x] Add product link on product card and product lists click.
	- [x] Image Carousel
	- [x] Main Info
	- [ ] Administration Panel
		- [x] Button Visual
		- [ ] Button Functionality
			- [ ] Edit product. Create page + implement form (Possibly reuse Create Product page)
			- [x] Delete Product
			- [x] Disable/Enable Product
			- [x] admin Stock
			- [x] Download product detail
	- [x] Complementary Info

- [ ] Implementar Tags/Characteristics product filter
	- [ ] Update `ProductSpecifications`
	- [ ] Modify FilterDTO (Tags IDs)
	- [ ] Special multi-accordion filters

- [ ] Implementar add product form functionality
	- [x] Crear S3 Bucket + Configurar
	- [x] Conectar frontend + backend para frontend image upload
	- [ ] Bug fixes: Unable to upload image to S3 and retrieve image URL for product creation.
		- [ ] 403 forbidden in OPTIONS AWS request

- [ ] Port All Services to AWS
	- [ ] Configure Backend AWS Image upload (Change Credentials + User IAM)
	- [ ] Create Backend JAR file (Maven)
		- [ ] Upload to EC2 Instance
	- [ ] Create Frontend build
		- [ ] Upload to Amplify instance
	- [ ] Ensure secure & correct connections between systems