# Reflection API

## 1) Преобразование сущностей

Есть два класса, которые имеют одинаковые значения, но разные представления.

1) Pet.java
```java
public class Pet {
    private String name;
    private Status status;
    private List<Photo> photosList;

    public Pet(String name, Status status, List<Photo> photosList) {
        this.name = name;
        this.status = status;
        this.photosList = photosList;
    }
}

enum Status {
    AVAILABLE,
    SOLD,
}

class Photo {
    private String name;
    private String URL;

    public Photo(String name, String URL) {
        this.name = name;
        this.URL = URL;
    }

    public String getName() {
        return name;
    }

    public String getURL() {
        return URL;
    }
}
```

2) Animal.java

```java
public class Animal {
    private String title;
    private boolean isAvailable;
    private boolean isSold;
    private Map<String, String> photosMap;

    @Override
    public String toString() {
       // Реализовать метод.
    }
}
```
Добавлять новые методы или менять модификаторы доступа нельзя.

Нужно создать метод, который преобразует класс Pet в Animal с помощью рефлексии.
В результате у класса Animal должны быть заполнены те же поля, что и в классе Pet

Пример:

```java
Pet cat = new Pet("Барсик", Status.AVAILABLE,
                List.of(new Photo("Барсик с цветочком",
                                "https://placekitten.com/200/300"),
                        new Photo("Барсик на ручках",
                                "https://placekitten.com/500/605")
                ));

Animal animalCat = mapToProductDto(cat);
System.out.println(animalCat);
```
Консоль:
```
Animal{
title='Барсик', 
isAvailable=true, 
isSold=false, 
photosMap={
Барсик на ручках=https://placekitten.com/500/605, 
Барсик с цветочком=https://placekitten.com/200/300}
}
```

## 2) Калькулятор через имена методов

Создайте интерфейс `Calculate`, который содержит произвольное количество методов (не менее 4-ёх)
которые возвращают `void` и имеют имена начинающиеся с `calc`, затем число, операцию над числом 
(sum, minus, multiply, divide) и второе чилсло.

Пример: 
```java
public interface Calculate {
    int calc1plus1();

    int calc100minus30();

    int calc25multiply5();

    int calc1000divide50();
}
```

Сделать метод, который в качестве параметра принимает интерфейс `Calculate` и выводит на экран
выражения описанные в методах вместе с ответом.

Пример
```
1 + 1 = 2
100 - 30 = 70
25 * 5 = 125
1000 / 50 = 20
```

