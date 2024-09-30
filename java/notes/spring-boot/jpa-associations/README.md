# [Map Associations with JPA and Hibernate (🔗)](https://thorben-janssen.com/ultimate-guide-association-mappings-jpa-hibernate/)

- [Introduction](#introduction)
- [Many-to-One Associations](#many-to-one-associations)
  - [Unidirectional Many-to-One Association](#unidirectional-many-to-one-association)
  - [Unidirectional One-to-Many Association](#unidirectional-one-to-many-association)
  - [Bidirectional Many-to-One Associations](#bidirectional-many-to-one-associations)
- [Many-to-Many Associations](#many-to-many-associations)
  - [Unidirectional Many-to-Many Associations](#unidirectional-many-to-many-associations)
  - [Bidirectional Many-to-Many Associations](#bidirectional-many-to-many-associations)
- [One-to-One Associations](#one-to-one-associations)
  - [Unidirectional One-to-One Associations](#unidirectional-one-to-one-associations)
  - [Bidirectional One-to-One Associations](#bidirectional-one-to-one-associations)

## Introduction

Association mapping model the relationship between 2 database tables as attributes in the domain model.

It allows easier navigation between entities in the domain model and JPQL.

You can map associations as a uni-or bidirectional relationship i.e., an attribute on 1 of the entities or on both. It has no impact on the database mapping, but it defines different directions to use the relationship.

## Many-to-One Associations

**Problem:** An order consists of multiple items, but each item belongs to only 1 order.

**Solution:** Store the primary key of the _Order_ record as a foreign key in the _OrderItem_ table.

- **Bidirectional Association:** an attribute on the _Order_ and _OrderItem_ entity.

- **Unidirectional Association:** an attribute on the _Order_ or _OrderItem_ entity.

### Unidirectional Many-to-One Association

The _OrderItem_ entity represents the many side of the relationship and its table contains the foreign key reference to the _Order_ table.

```java
@Entity
public class OrderItem {

    @ManyToOne
    private Order order; // models the association

}
```

By default, generates Hibernate the name of the foreign key based on the name of the:

- relationship mapping attribute (**order**)
- primary key attribute **id**

To define a custom foreign key column name, use the `@JoinColumn` annotation.

```java
@ManyToOne
@JoinColumn(name = “fk_order”)
private Order order;
```

Use the association in your business code.

```java
Order order = em.find(Order.class, 1L);

OrderItem orderItem = new OrderItem();
orderItem.setOrder(order);

entityManager.persist(orderItemi);
```

[Dive Deeper: Tutorial on defining FetchTypes.](https://thorben-janssen.com/entity-mappings-introduction-jpa-fetchtypes/)

### Unidirectional One-to-Many Association

The unidrectional 1-to-many mapping is not every common. It should be avoided in your domain model, otherwise Hibernate might create unexpected tables and execute more SQL statements than you expected.

### Bidirectional Many-to-One Associations

The most common way to model the relationship in the problem shown above.

It uses an attribute on the _Order_ and _OrderItem_ entity, which allows to navigate the association in both directions in the domain model/JPQL.

It consists of 2 parts

- the to-many side which owns the relationship mapping
- the to-one side which references the mapping

The owning side (to-many), which provides all the information Hibernate needs to map it to the database:

```java
@Entity
public class OrderItem {

    @ManyToOne
    @JoinColumn(name = “fk_order”)
    private Order order;

}
```

The referencing side (to-one), which simply references the owning side by providing the name of the association-mapping attribute to the `mappedBy` attribute of the `@ManyToOne` annotation.

```java
@Entity
public class Order {

    @OneToMany(mappedBy = “order”)
    private List<OrderItem> items;

}
```

Adding/removing an entity requires an additional step:

```java
@Entity
public class Order {
    ...

    public void addItem(OrderItem item) {
        this.items.add(item);
        item.setOrder(this);
    }

    ...
}

Order order = em.find(Order.class, 1L);
OrderItem item = new OrderItem();
order.addItem(item);
em.persist(i);
```

## Many-to-Many Associations

On the database level, it requires an additional _association table_ which contains the primary key pairs of the associated entities.

**Problem:** Each store sells multiple products and each Product gets sold in multiple stores.

**Solution:** You can model a many-to-many association as a uni-or bidirectional relationship between 2 entities.

However, a `Set` should be used instead of a `List` as the attribute type. Otherwise, Hibernate will inefficiently remove entities from the association by removing all records from the _association table_ and re-inserting remaining ones.

### Unidirectional Many-to-Many Associations

The relationship mapping requires both

- an entity attribute that models the association in the domain model
- a `@ManyToMany` annotation that tells Hibernate to map it as a many-to-many association (table).

```java
@Entity
public class Store {

    @ManyToMany
    private Set<Product> products = new HashSet<Product>();

}
```

By default, Hibernate uses its mapping which expects an association table with the name of both entities and the primary key attributes of both entities.

This can be customised with a `@JoinTable` annotation and its attributes:

- `joinColumns` defines the foreign key columns for the entity on which you define the assocation mapping.
- `inverseJoinColumns` specifies the foreign key columns of the associated entity.

```java
@Entity
public class Store {

    @ManyToMany
    @JoinTable(name = “store_product”,
           joinColumns = { @JoinColumn(name = “fk_store”) },
           inverseJoinColumns = { @JoinColumn(name = “fk_product”) })
    private Set<Product> products = new HashSet<Product>();

}
```

### Bidirectional Many-to-Many Associations

One entity owns the association and provides all mapping information, while the other entity references the mapping assocation.

Owning side

```java
@Entity
public class Store {

    @ManyToMany
    @JoinTable(name = “store_product”,
           joinColumns = { @JoinColumn(name = “fk_store”) },
           inverseJoinColumns = { @JoinColumn(name = “fk_product”) })
    private Set<Product> products = new HashSet<Product>();

}
```

Referencing side

```java
@Entity
public class Product{

    @ManyToMany(mappedBy=”products”)
    private Set<Store> stores = new HashSet<Store>();

}
```

You need to update both ends of a bidirectional association when you want to add or remove an entity.

```java
@Entity
public class Store {

    public void addProduct(Product p) {
        this.products.add(p);
        p.getStores().add(this);
    }

    public void removeProduct(Product p) {
        this.products.remove(p);
        p.getStores().remove(this);
    }

}
```

## One-to-One Associations

One-to-one relationships are rarely used in relational table models, hence it won't be needed often, but it's good to know how to map them.

**Problem:** Each _Customer_ has exactly one _ShippingAddress_ and each _ShippingAddress_ belongs to one _Customer_.

**Solution:** On the database level, this is mapped by a foreign key column either on the _ShippingAddress_ or the _Customer_ table.

### Unidirectional One-to-One Associations

Model for the entity for which you want to navigate the relationship in your domain model/query e.g., from _Customer_ to _ShippingAddress_ entity.

```java
@Entity
public class Customer {

    @OneToOne
    @JoinColumn(name = “fk_shippingaddress”) // optional
    private ShippingAddress shippingAddress;

}
```

```java
Customer c = em.find(Customer.class, 1L);
ShippingAddress sa = c.getShippingAddress();
```

### Bidirectional One-to-One Associations

It's also modelled on the _ShippingAddress_ entity so that you can get the _Customer_ for a giving _ShippingAddress_.

Owning side (can specify custom foreign key column name):

```java
@Entity
public class Customer{

    @OneToOne
    @JoinColumn(name = “fk_shippingaddress”)
    private ShippingAddress shippingAddress;

}
```

Referencing side (define mappedBy attribute of the @OneToOne annotation):

```java
@Entity
public class ShippingAddress{

    @OneToOne(mappedBy = “shippingAddress”)
    private Customer customer;

}
```
