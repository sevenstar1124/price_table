Hello, I need a single HTML template designed to replace an aging price checker screen.
The price checker itself scans a barcode and passes it to a web server, product and price data is queried and sent to an HTML template with some CSS styles for viewing by the customer.
I need you to create a new modern HTML template that is responsive to screen orientation and includes things like the product image, name, description, price, sale information, etc. without needing to scroll (fixed size, no user interaction). Think of it like a kiosk display image.
I can supply the current page we're using so you can get an idea of what we're starting with.
Please note I have the back end all developed and finished, this task is solely for creating a single HTML template that is designed to be modern and responsive for phones/tablets with no scrolling.

Thank you Vladyslav this looks very elegant and professional but has the appearance of a formal event invite instead of an art store. can you please check my message above it contains the html template with the {{ variables }} included. can you please incorporate these variables into your code. also please remove the other images just need the product picture. please increase the size of the pricing, the users attention should be drawn to the price first. if you check the template code above youll see different stylings if the product is on sale or not.
also feel free to use some colour for example if the product is on sale perhaps add a light red shaded background behind the price/text
overall i like the framework though it's responsive and layouts correctly in both orientations


<body>
	{% if not product.product_name %}
		<div class="container">
			<h1 class="header">Sorry product not found</h1>
		</div>
	{% else %}
		<div class="container">
			<h1 class="header">{{ product.product_name }}</h1>
			<hr style="margin-bottom:5px;"/>
			<div class="middle-section">
				<img src="{{ product.image_url | safe }}" alt="Product Image">
				<div class="product-specifications">
					{% if product.sale_active is true %}
						<p class="sale-border"><span class="label">ON SALE: </span><span class="value">${{ product.sale_price }}</span><br><span class="label"> (Ends: {{ product.sale_end }})</span></p>
						<p><span class="label">Delta's Price: </span><span class="value">${{ product.delta_price }}</span></p>
					{% else %}
						<p class="sale-border value"><span class="label">Delta's Price: </span><span class="value">${{ product.delta_price }}</span></p>
					{% endif %}
					<p><span class="label">Regular Price: </span><span class="value">${{ product.regular_price }}</span></p>
					<p><span class="label">SKU: </span><span class="value">{{ product.product_code }}</span></p>
				</div>
				{% set truncated_description = product.description[:500] %}
				<div class="product-description">
					{% if product.description|length > 500 %}
						<p>{{ truncated_description }}...</p>
					{% else %}
						<p>{{ product.description }}</p>
					{% endif %}
				</div>
			</div>
		</div>
	{% endif %}
</body>

