```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Unicorn {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;
    private String name;
    private int age;
    private int powerStrength;

    // Getters and setters
}
```

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;

public class UnicornDAO {

    private EntityManagerFactory entityManagerFactory = Persistence.createEntityManagerFactory("UnicornApp");
    private EntityManager entityManager = entityManagerFactory.createEntityManager();

    public void save(Unicorn unicorn) {
        entityManager.getTransaction().begin();
        entityManager.persist(unicorn);
        entityManager.getTransaction().commit();
    }

    public Unicorn findById(int id) {
        return entityManager.find(Unicorn.class, id);
    }

    public Unicorn update(Unicorn unicorn) {
        entityManager.getTransaction().begin();
        Unicorn updatedUnicorn = entityManager.merge(unicorn);
        entityManager.getTransaction().commit();
        return updatedUnicorn;
    }

    public void delete(int id) {
        entityManager.getTransaction().begin();
        Unicorn unicorn = findById(id);
        if (unicorn != null) {
            entityManager.remove(unicorn);
        }
        entityManager.getTransaction().commit();
    }

    public void close() {
        entityManager.close();
        entityManagerFactory.close();
    }
}

```

```java
public class Main {
    public static void main(String[] args) {
        UnicornDAO unicornDAO = new UnicornDAO();

        // Create
        Unicorn newUnicorn = new Unicorn();
        newUnicorn.setName("Sparkle");
        newUnicorn.setAge(5);
        newUnicorn.setPowerStrength(90);
        unicornDAO.save(newUnicorn);

        // Read
        Unicorn foundUnicorn = unicornDAO.findById(1);
        System.out.println("Found Unicorn: " + foundUnicorn.getName());

        // Update
        foundUnicorn.setAge(6);
        Unicorn updatedUnicorn = unicornDAO.update(foundUnicorn);
        System.out.println("Updated Unicorn Age: " + updatedUnicorn.getAge());

        // Delete
        unicornDAO.delete(1);

        unicornDAO.close();
    }
}

```