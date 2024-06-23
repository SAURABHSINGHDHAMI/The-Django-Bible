# Database Schema Design and Relationships: One-to-One, One-to-Many, Many-to-Many

## Project Planning and Execution

<p align="center">
  <img src="https://github.com/SAURABHSINGHDHAMI/The-Django-Bible/assets/95751390/f1373c63-0443-4ca5-843c-945c203a3029" alt="The Django Bible">
</p>

### Overview

Before starting any project, it is essential to have a clear plan and follow systematic steps to ensure successful execution. The following steps outline the process:

### Steps to Execution

1. **Requirement Analysis**
2. **User Cases & User Stories**
3. **Workflow Design**
4. **Basic Wireframe**
5. **Designing**
6. **Database Schema**

### Handling Different Types of Relationships in Django

#### One-to-One Relationship

- **Example**: In an e-commerce website, there are two tables, User and Cart. Each User has one Cart, and each Cart is assigned to only one User.
- **Implementation**: Use `OneToOneField` in Django models.

#### One-to-Many Relationship (ForeignKey)

- **Example**: A Cart can have multiple products, and a Product can be in multiple carts.
- **Tables**:
  - **Cart**: Contains cart details.
  - **Product**: Contains product details.
  - **ProductInCart**: Links Cart and Product with quantity.
  ```python
  class Cart(models.Model):
      user = models.OneToOneField(User, on_delete=models.CASCADE)
  
  class Product(models.Model):
      name = models.CharField(max_length=100)
  
  class ProductInCart(models.Model):
      cart = models.ForeignKey(Cart, on_delete=models.CASCADE)
      product = models.ForeignKey(Product, on_delete=models.CASCADE)
      quantity = models.IntegerField()
      class Meta:
          unique_together = ('cart', 'product')
  ```

#### Many-to-Many Relationship

- **Example**: A User can play multiple Instruments, and an Instrument can be played by multiple Users.
- **Implementation**: Use `ManyToManyField` in Django models.
  ```python
  class User(models.Model):
      name = models.CharField(max_length=100)
      instruments = models.ManyToManyField('Instrument', related_name='players')
  
  class Instrument(models.Model):
      name = models.CharField(max_length=100)
  ```

### Django Model Fields

#### Common Fields

- `CharField`: For short text fields.
- `TextField`: For large text fields.
- `IntegerField`: For integer values.
- `FloatField`: For floating-point numbers.
- `DateTimeField`: For date and time.
- `BooleanField`: For boolean values.

#### Options Fields

- Enum-like choices for status fields, such as:
  ```python
  STATUS_CHOICES = [
      ('NP', 'Not Packed'),
      ('IT', 'In Transit'),
      ('S', 'Shipped'),
      ('D', 'Delivered'),
  ]
  
  class Order(models.Model):
      status = models.CharField(max_length=2, choices=STATUS_CHOICES)
  ```
