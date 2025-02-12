# co.hotwax.sob.product.ProductMappingServices.map#ProductVariant (shopify-oms-bridge)
1. Service Parameters
    * Input
        * shopifyProductVariant
        * shopId
        * forCreate (Boolean)
    * Output
        * productVariant
2. Get productIdentifierEnumId from ProductStore associated to shopId, based on returned value set productIdentifier = shopifyProductVariant.id OR shopifyProductVariant.sku OR shopifyProductVariant.barcode
3. Initialize productVariant map
4. Check if product already exists, set productVariant.productId = get Product.productId from Product where Product.internalName = producIdentifier.
5. If productVariant.productId exists and forCreate=true, we will only create ShopifyShopProduct record and not setup complete product
    * Set productVariant.shopifyShopProduct = [shopId:shopId, shopifyProductId:shopifyProduct.id, shopifyInventoryItemId:shopifyProductVariant.inventoryItem.id]
    * return
6. Prepare productVariant map
    * productVariant.internalName = productIdentifier
    * productVariant.productTypeId
        * default to FINISHED_GOOD
        * if shopifyProductVariant.inventoryItem.requireShipping=false, set as DIGITAL_GOOD
        * if shopifyProductVariant.requiresComponents=true, set as MARKETING_PKG_PICK
    * productVariant.productName = shopifyProductVariant.title
    * productVariant.detailImageUrl = shopifyProductVariant.image.url
    * productVariant.primaryCategoryId = browse root category of the ProductStore associated with shopId (write helper method/service as needed)
    * productVariant.weight = shopifyProductVariant.inventoryItem.measurement.value
    * productVariant.shippingWeight = shopifyProductVariant.inventoryItem.measurement.value
    * productVariant.weightUomId = uomId where shopifyProductVariant.inventoryItem.measurement.unit = Uom.abbreviation
    * productVariant.isVirtual = N
    * productVariant.isVariant = Y
    * productVariant.sequenceNum = shopifyProductVariant.position
    * productVariant.prices = Check if ProductPrice exists. If yes set [[productPriceTypeId:"LIST_PRICE", productPricePurposeId:"PURCHASE", currencyUomId:ProductStore.defaultCurrencyUomId, price:shopifyVariant.price,productStoreGroupId:ProductStore.primaryStoreGroupId, fromDate:ProductPrice.fromDate]] else set [[productPriceTypeId:"LIST_PRICE", productPricePurposeId:"PURCHASE", currencyUomId:ProductStore.defaultCurrencyUomId, price:shopifyVariant.price,productStoreGroupId:ProductStore.primaryStoreGroupId]]
    * productVariant.features = iterate through shopifyProductVariant.selectedOptions and add [productFeatureTypeDesc:shopifyProductVariant.selectedOptions.name, featureDesc:shopifyProductVariant.selectedOptions.value, productFeatureApplTypeId:'STANDARD_FEATURE', sequenceNum:shopifyProductVariant.position]
        * productFeatureId = set if exists
        * productFeatureApplTypeId = "STANDARD_FEATURE"
        * productFeatureTypeId = shopifyProductVariant.selectedOptions.name
        * description = shopifyProductVariant.selectedOptions.value
        * sequenceNum = shopifyProductVariant.position
    * productVariant.identifications = add following key value pairs to the list
        * Check if GoodIdentification exists for productVariant.productId and goodIdentificationTypeId="SHOPIFY_PROD_SKU". If yes add [goodIdentificationTypeId: "SHOPIFY_PROD_SKU", idValue=productVariant.sku, fromDate:GoodIdentification.fromDate] else add [goodIdentificationTypeId: "SHOPIFY_PROD_SKU", idValue=productVariant.sku]
        * Check if GoodIdentification exists for productVariant.productId and goodIdentificationTypeId="UPCA". If yes add [goodIdentificationTypeId: "UPCA", idValue=productVariant.barcode, fromDate:GoodIdentification.fromDate] else add [goodIdentificationTypeId: "UPCA", idValue=productVariant.barcode]
    * productVariant.shopifyShopProduct = [shopId:shopId, shopifyProductId:shopifyProductVariant.id, shopifyInventoryItemId:shopifyProductVariant.inventoryItem.id]