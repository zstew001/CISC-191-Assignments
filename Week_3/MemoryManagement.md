```java

class Person {
    int id;
    String name;


    public Person(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

public class PersonBuilder {
    private static Person buildPerson(int id, String name) {
        return new Person(id, name);
    }

    public static void main(String[] args) {
        int id = 23;
        String name = "John";
        Person person = null;
        person = buildPerson(id, name);
    }
}
```
![IMG_2444](https://github.com/user-attachments/assets/5cce2d46-c85c-4dbc-aa33-d8e5184cab01)
