# Fully Customize Django Models: Exploring Models, Model Managers, and Shell

## Models

### Product Model

The `Product` model includes methods for updating the price and creating new products. These methods demonstrate the use of `@classmethod` and `@staticmethod`.

```python
from django.db import models

class Product(models.Model):
    product_id = models.AutoField(primary_key=True)
    product_name = models.CharField(max_length=255)
    price = models.FloatField()

    @classmethod
    def update_price(cls, product_id, price):
        product = cls.objects.filter(product_id=product_id).first()
        product.price = price
        product.save()
        return product
    
    @classmethod
    def create(cls, product_name, price):
        product = cls(product_name=product_name, price=price)
        product.save()
        return product
    
    def __str__(self):
        return self.product_name
```

### Using Django Shell with Product Model

```sh
$ python manage.py shell
```

```python
from app.models import Product

# Fetch all products
p = Product.objects.all()

# Get the first product
p = p.first()

# Print the product_id
print(p.product_id)

# Update the price of product with product_id 4 to 3000
Product.update_price(4, 3000)

# Check the price
p.price

# Update the price of product with product_id 4 to 2000
Product.update_price(4, 2000)

# Fetch the first product again
p = Product.objects.all().first()

# Check the price again
p.price

# Create a new product
p2 = Product.create("toy car", 2000)

# Get the last product
p3 = Product.objects.all().last()

# Print the product
print(p3)

# Print the product_id of the last product
p3.product_id
```

## Model Managers

### CartManager and Cart Model

The `CartManager` class includes a method for creating a cart. This method can include additional operations beyond creating the cart.

```python
from django.db import models
from django.contrib.auth.models import User

class CartManager(models.Manager):
    def create_cart(self, user):
        cart = self.create(user=user)
        # additional operations can be performed here
        return cart

class Cart(models.Model):
    cart_id = models.AutoField(primary_key=True)
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    created_on = models.DateTimeField(auto_now_add=True)

    objects = CartManager()
```

### Using Django Shell with Cart Model

```sh
$ python manage.py shell
```

```python
from app.models import Cart
from django.contrib.auth.models import User

# Get the first user
user = User.objects.all().first()

# Print the user
print(user)

# Get the first cart
cart = Cart.objects.all().first()

# Print the cart
print(cart)

# Delete the cart
cart.delete()

# Verify the cart is deleted
cart = Cart.objects.all().first()
print(cart)

# Create a new cart for the user
c = Cart.objects.create_cart(user=user)

# Print the newly created cart
print(c)
```

## Database Entry Using Django Shell

### Creating and Updating Products

```sh
$ python manage.py shell
```

```python
from app.models import Product

# Create a new product
p = Product.objects.create(product_name="iphone", price=100000)
print(p)

# Create another product using save method
p2 = Product(product_name="samsung s22", price=100000)
p2.save()

# Fetch all products
Product.objects.all()

# Update the price of the second product
p2.price = 50000
p2.save()
```

## Understanding Save and Update in Django

When creating a new object and saving it, Django generates a primary key (pk) or ID. When an instance is later retrieved and saved again, Django checks for the primary key. If found, it updates the existing record; if not, it saves a new entry in the database.
