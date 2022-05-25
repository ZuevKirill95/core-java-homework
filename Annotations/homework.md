# Аннотации

Создайте класс, в котором будут методы (не менее 4-ёх), возвращающие какую-нибудь строку.

Пример

```java
class Messages {
    public String happyBirthday() {
        return "С днём рождения!";
    }

    public String warning() {
        return "Предупреждение";
    }

    public String error() {
        return "Ошибка";
    }
}
```


Реализуйте аннотацию `@Paint` которая будет иметь два поля 
* `style`, где вы задаете стиль, в котором будет выводится строка. (Наименование и сам стиль может быть любым)
* `color`, цвет, которым будут выводится строка.

Для вывода текста в цвете можете использовать следующие константы
```java
public static final String RESET = "\u001B[0m";
public static final String BLACK = "\u001B[30m";
public static final String RED = "\u001B[31m";
public static final String GREEN = "\u001B[32m";
public static final String YELLOW = "\u001B[33m";
public static final String BLUE = "\u001B[34m";
public static final String PURPLE = "\u001B[35m";
public static final String CYAN = "\u001B[36m";
public static final String WHITE = "\u001B[37m";
```
Вывод в цвете пишется так:

```java
System.out.println(ANSI_RED + "This text is red!" + ANSI_RESET);
```

Аннотация должна быть применима к классу и методу. Приоритет у аннотации метода.

Пример:

```java
@Print(style = "arrow", color = RED)
class Messages {
    @Print(style = "hurray", color = PURPLE)
    public String happyBirthday() {
        return "С днём рождения!";
    }

    @Print(style = "!", color = YELLOW)
    public String warning() {
        return "Предупреждение";
    }
    
    public String error() {
        return "Ошибка";
    }
}

// Метод для вывода сообщений в консоль (его нужно реализовать)
print(new Messages())
```
Вывод в консоли:

<span style="color:purple"> \/\/\/ С днём рождения! \/\/\/</span>

<span style="color:yellow">!!! Предупреждение !!!</span>

<span style="color:red">---> Ошибка <---</span>



