# Parent/Child Interaction Solution

## Preqruisites
1. **[Angular CLI Installed](https://github.com/angular/angular-cli#installation)**

## Setup and Run	
1. Setup the application: `npm install`
1. Run the application: `npm run start`

## Solution Steps
1. Create product directory
1. Move product.model under product directory

### Dumb Component ProductListComponent
1. Create and Initialize ProductListComponent, template, and css files
	* selector: product-list
	* Since this is a dumb component, set the ChangeDetectionPolicy to OnPush
1. Declare the ProductListComponent w/ the AppModule
1. Inside the ProductList template: 
	* Copy the Products Header HTML from app.component.html to product-list.component.html
	* Copy the Products *ngFor HTML from app.component.html to product-list.component.html
		* Remove the [class.selected] as produts and produt details will not be shown together anymore
	* Move the Create New Product button from app.component.html and insert & style it next to the Products Header
1. In product-list.component, add an @Input products property to take in list of products
1. In product-list.component, add an @Output event property to emit an onSelected event of product.id
1. In product-list.component, add an @Output event property to event an onNewClick event
1. Adjust the product-list.component template, to emit these event upon click
1. Copy the trackByProduts from app.component, to product-list

### Dumb Component ProductDetailsComponent
1. Create and Initialize ProductDetailsComponent, template, and css files
	* selector: product-details
	* Since this is a dumb component, set the ChangeDetectionPolicy to OnPush
1. Declare the ProductDetailsComponent w/ the AppModule
1. Inside the ProductDetails template: 
	* Copy the ProductDetails Header HTML from app.component.html to product-details.component.html
		* Do Not copy the Create New Product button as we did that already above in Product List
	* Copy the ProductDetails input fields, save button, and cancel button HTML from app.component.html to product-details.component.html
	* Remove the *ngIf to display the input fields and buttons
1. In product-details.component, add an @Input item property to take in a product
	* Fix the product-details.component.template to use item
1. In product-details.component, add an @Output event property to emit an onSaveClick event of item
1. In product-details.component, add an @Output event property to event an onCancelClick event


### Smart Component ProductsComponent
1. Create and Initialize ProductsComponent and Template
	* selector: products
1. Declare the ProductsComponent w/ the AppModule
1. In products.component, define and initialze the array of products that is in the app.component
1. In products.component, define a selectedProduct of type Product
1. In products.component.html, define the relationship to the child components
	* `<product-details></product-details>` for the ProductDetailsComponent
	* `<product-list></product-list>` for the ProductListComponent
	* `*ngIf` that product details will be shown if selectedProduct has a value, otherwise product list
	* Property Bind to the appropriate input properties for each
		* `<product-details [item]="selectedProduct">`
		* `<product-list [products]="productList">`
	* Event Bind to the appropriate output properties for each with the template statements of your preference
		* onSaveClick and onCancelClick: `<product-details (onSaveClick)="saveProductHandler($event)" (onCancelClick)="selectedProduct = null">`
		* onSelected and onNewClick: `<product-list (onSelected)="selectedProductHandler($event)" (onNewClick)="newProductHandler()">`
		* Copy and adjust the event handlers from app.component and put them into products.component

### Refactor AppComponent to be the parent component of Products
1. Remove all the code from app.component except the initialzation of the AppComponent class
1. Remove all the product HTML and instead instantiate the child relationship `<products></products>`

### Create Product Feature Module
1. Create product.module
	* Set imports: CommonModule
	* Set declarations: ProductsComponent, ProductDetailsComponent, ProductListComponent
	* Set exports: ProductsComponent
1. In the app.module, remove reference to the Product*Component
1. In the app.module, add an import for ProductModule	
