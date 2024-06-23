# Implementing Database Design in Django: Models, Migrations, Model Relationships, and Field Types

## Models

### models.py

```python
from django.db import models
from django.contrib.auth.models import User

# Create your models here.

class Product(models.Model):
    product_id = models.AutoField(primary_key=True)
    product_name = models.CharField(max_length=255)
    price = models.FloatField()

    def __str__(self):
        return self.product_name

class Cart(models.Model):
    cart_id = models.AutoField(primary_key=True)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    created_on = models.DateTimeField()

class ProductInCart(models.Model):
    product_in_cart_id = models.AutoField(primary_key=True)
    cart = models.ForeignKey(Cart, on_delete=models.CASCADE)
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    quantity = models.PositiveIntegerField()

    class Meta:
        unique_together = ('cart', 'product')

class Order(models.Model):
    NOT_PACKED = 1
    READY_FOR_SHIPPING = 2
    SHIPPED = 3
    DELIVERED = 4

    STATUS_CHOICES = (
        (NOT_PACKED, 'Not Packed'),
        (READY_FOR_SHIPPING, 'Ready For Shipping'),
        (SHIPPED, 'Shipped'),
        (DELIVERED, 'Delivered'),
    )

    user = models.ForeignKey(User, on_delete=models.CASCADE)
    status = models.IntegerField(choices=STATUS_CHOICES, default=NOT_PACKED)
```

- The models we create in `models.py` are common among all databases in a Django project.

- Django's ORM (Object-Relational Mapping) allows easy migrations over different databases.

- Different databases have different commands to create tables, but Django provides a common syntax for all databases via ORM.

- The ORM converts queries performed in Django into the respective database queries.

### Migrations

To apply the changes in your models to the database, run the following commands:

```bash
py manage.py makemigrations
py manage.py migrate
```

## Admin Interface

### admin.py

```python
from django.contrib import admin
from .models import Cart, Product, ProductInCart, Order

# Register your models here.

admin.site.register(Cart)
admin.site.register(Product)
admin.site.register(ProductInCart)
admin.site.register(Order)
```

### Steps to Use Admin Interface

1. Create a superuser:

    ```bash
    py manage.py createsuperuser
    ```

2. Run the server:

    ```bash
    py manage.py runserver
    ```

3. Access the admin panel at `http://127.0.0.1:8000/admin/`.

## Performing Database Operations

You have three options for making database entries and performing queries:

1. Django Admin Panel
2. Django Shell
3. Raw Code

- The Django ORM abstracts database interactions and provides a common API regardless of the underlying database.

- This ensures that you can switch databases easily without changing your code.

- Use the admin interface for quick data entry and management during development.
