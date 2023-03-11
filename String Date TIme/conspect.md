# Строки, дата и время

## Строка

Объект `String` инкапсулирует последовательность символов `Unicode*`.
Во внутреннем представлении эти символы хранятся в обычном массиве Java.

> Unicode (Юникод) — стандарт кодирования символов, включающий в себя знаки почти всех письменных языков мира. В
> настоящее время стандарт является преобладающим в Интернете.

`String` являются неизменяемыми (immutable); после того, как вы создадите объект String, изменить его значение уже не
удастся.

```java
class Main {
    public static void main(String[] args) {
        String str = "Hello"; // Создание объекта
        str = str + " World!"; // Повторное создание объекта
    }
}
```

## Многострочное создание строки

```java
class Main {
    public static void main(String[] args) {
        String borodino =
                "— Скажи-ка, дядя, ведь недаром\n" +
                        "Москва, спаленная пожаром,\n" +
                        "Французу отдана?\n";
    }
}
```

java 15+ (text-blocks)

```java
class Main {
    public static void main(String[] args) {
        String borodino =
                """
                        — Скажи-ка, дядя, ведь недаром
                        Москва, спаленная пожаром,
                        Французу отдана?
                        """;
    }
}
```

## Создание строк по другим данным

Строковое представление значения можно получить при помощи статического метода `String.valueOf()`.

### Примитивные типы

```java
class Main {
    public static void main(String[] args) {
        String one = String.valueOf(1); // "1"
        String two = String.valueOf(2.384f); // "2.384"
        String notTrue = String.valueOf(false); // "false"
    }
}
```

### Объекты

```java
class Main {
    public static void main(String[] args) {
        Date date = new Date();
        String d1 = String.valueOf(date); // "Fri Dec 19 05:45:34 CST 1969"
        String d2 = date.toString(); // "Fri Dec 19 05:45:34 CST 1969"

        date = null;
        d1 = String.valueOf(date); // "null"
        d2 = date.toString(); // NullPointerException!
    }
}
```

## Сравнение строк

`equals()`

```java
class Main {
    public static void main(String[] args) {
        String one = "ПРИВЕТ";
        String two = "привет";

        one.equals(two); // false
        one.equalsIgnoreCase(two); // true
    }
}
```

> Важно!
>
> Не сравнивайте с помощью оператора сравнения (==)! Сравнение может быть некорректным

`compareTo()`

```java
class Main {
    public static void main(String[] args) {
        String andrey = "Андрей";
        String yana = "Яна";
        String num = "123";

        System.out.println(andrey.compareTo(yana) < 0); // true
        System.out.println(andrey.compareTo(andrey) == 0); // true
        System.out.println(andrey.compareTo(num) > 0); // true
    }
}
```

## Другие полезные методы

Со всеми методами можно ознакомится в
[документации](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)

```java
class Main {
    public static void main(String[] args) {
        String url = "https://online.sberbank.ru";
        url.startsWith("https:"); // true
        url.endsWith("ru"); // true
        url.contains("sberbank"); // true
        url.indexOf("online"); // 8
        url.charAt(8); // 'o'

        String emptyString = "    ";
        emptyString.isEmpty(); // false. Возвращает true, если строка имеет нулевую длину
        emptyString.isBlank(); // true. Возвращает true, если строка имеет нулевую длину или содержит только пробелы

        String username = "   user_123   ";
        username.trim(); // "user_123"

        String attention = "внимание";
        attention.toUpperCase(); // "ВНИМАНИЕ"

        String java = "JAVA";
        attention.toLowerCase(); // "java"
    }
}
```

## Регулярные выражения

Регулярные выражения – это мощный инструмент для поиска и замены слов в тексте. Само регулярное выражение представляет
собой обычную строку, составленную по определенным правилами. В общем виде она представляет собой две косые
черты `/ /`, где после первой черты идёт специальный паттерн для поиска, а после второй – набор флагов.

Для тренировки использования регулярных выражений можно воспользоваться сайтом [Regex101.com](https://regex101.com/).

[Шпаргалка по регулярным выражениям](https://github.com/cheatsnake/backend-cheats/blob/master/files/programming-language/regex-cheatsheet.md)

## API регулярных выражений

Регулярное выражение, указанное в виде строки, должно быть сначала скомпилировано в экземпляр класса `Pattern`.
Полученный шаблон затем можно использовать для создания `Matcher` объекта, который может сопоставлять произвольные
последовательности символов с регулярным выражением.

```java
class Main {
    public static void main(String[] args) {
        Pattern p = Pattern.compile("a*b");
        Matcher m = p.matcher("aaaaab");
        boolean b = m.matches(); // true
    }
}
```

### Класс `Pattern`

`Pattern` - Скомпилированное представление регулярного выражения.

Со всеми методами можно ознакомится в
[документации](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/regex/Pattern.html)

- `static Pattern compile(String regex)` - Компилирует заданное регулярное выражение в шаблон (pattern).

- `static Pattern compile(String regex, int flags)` - Компилирует заданное регулярное выражение в шаблон (pattern) с
  заданными флагами.

```java
class Main {
    public static void main(String[] args) {
        // Поиск подстроки "java"
        Pattern pattern1 = Pattern.compile("java");
        // Поиск подстроки "java" с игнорированием регистра
        Pattern pattern2 = Pattern.compile("java", Pattern.CASE_INSENSITIVE);
    }
}
```

- `static boolean matches(String regex, CharSequence input)` - Компилирует заданное регулярное выражение и пытается
  сопоставить с ним заданное входное значение.

```java
class Main {
    public static void main(String[] args) {
        Pattern.matches("\\d+\\.\\d+f?", "42.0f"); // true 
        Pattern.matches("\\d+\\.\\d+f?", "42.0"); // true
        Pattern.matches("\\d+\\.\\d+f?", "42"); // false
    }
}
```

### Класс `Matcher`

`Matcher` - Механизм, который выполняет операции сопоставления строки с шаблоном регулярного выражения (`Pattern`).

Со всеми методами можно ознакомится в
[документации](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/regex/Matcher.html)

Создание объекта `Matcher`

- `Matcher matcher(CharSequence input)` - Метод класса `Pattern`. Создает `Matcher`, который будет сопоставлять заданную
  строку с этим шаблоном

```java
class Main {
    public static void main(String[] args) {
        Pattern p = Pattern.compile("a*b");
        Matcher m = p.matcher("aaaaab");
    }
}
```

- `boolean find()` - Пытается найти следующую последовательность входной строки, которая соответствует шаблону.
- `int start()` - Возвращает начальный индекс предыдущего совпадения.
- `int end()` - Возвращает индекс после последнего совпадающего символа.
- `String replaceFirst(String replacement)` - Заменяет первое совпадение с регулярным выражением, на указанную строку.
- `String replaceAll(String replacement)` - Заменяет все совпадения с регулярным выражением, на указанную строку.

```java
class Main {
    public static void main(String[] args) {
        String text = "Егор Алла Анна";
        Pattern pattern = Pattern.compile("А.+?а");

        Matcher matcher = pattern.matcher(text);

        while (matcher.find()) {
            int start = matcher.start();
            int end = matcher.end();
            System.out.println("Найдено совпадение " + text.substring(start, end) + " с " + start + " по " + (end - 1) + " позицию");
        }
        // Найдено совпадение Алла с 5 по 8 позицию
        // Найдено совпадение Анна с 10 по 13 позицию


        System.out.println(matcher.replaceFirst("Ира")); // Егор Ира Анна
        System.out.println(matcher.replaceAll("Ольга")); // Егор Ольга Ольга
        System.out.println(text); // Егор Алла Анна
    }
}
```

## Дата и время

### Класс `LocalDate`

`LocalDate` - представляет дату без информации о времени для вашего региона (например, 4 мая 2019 года).

```java
class Main {
    public static void main(String[] args) {
        LocalDate.now(); // Текущая дата (Например 2023-03-11)

        LocalDate.of(2019, 5, 4); // 2019-05-04
        LocalDate.parse("2019-05-04"); // 2019-05-04
    }
}
```

### Класс `LocalTime`

`LocalTime` - представляет время без информации о дате (например, 7:15)

```java
class Main {
    public static void main(String[] args) {
        LocalTime.now(); // Текущее время (Например 14:19:06.698532700)

        LocalTime.of(7, 15); // 07:15
        LocalTime.parse("07:15"); // 07:15
    }
}
```

### Класс `LocalDateTime`

`LocalDateTime` - хранит и дату и время

```java
class Main {
    public static void main(String[] args) {
        LocalDateTime.now(); // Текущая дата и время (Например 2023-03-11T14:21:10.273589800)

        LocalDateTime.of(2019, 5, 4, 7, 0);
        LocalDateTime.parse("2019-05-04T07:15");
    }
}
```

### Другие полезные методы

```java
class Main {
    public static void main(String[] args) {
        LocalDate today = LocalDate.now(); // 2019-12-12
        // Добавляем одну неделю
        LocalDate reminder = today.plus(1, ChronoUnit.WEEKS); // 2019-12-19

        LocalTime first = LocalTime.of(7, 15); // 07:15
        LocalTime second = LocalTime.of(10, 30); // 10:30
        first.isBefore(second); // true
        ChronoUnit.HOURS.between(first, second); // false
    }
}
```

[//]: # (TODO: Часовые пояса ZonedDateTime и OffsetDateTime)

### Разбор и форматирование даты и времени

Дата и время по умолчанию отображается по [стандартам ISO](https://ru.wikipedia.org/wiki/ISO_8601)

Для работы с нестандартными отображениями используйте `DateTimeFormatter`

```java
class Main {
    public static void main(String[] args) {
        DateTimeFormatter shortRU = DateTimeFormatter.ofPattern("dd.MM.yy");

        LocalDate valentinesDay = LocalDate.parse("14/02/19", shortRU); // 2019-02-14

        LocalDate today = LocalDate.now(); // 2019-12-14
        shortRU.format(today); // "14/12/19"
    }
}
```

### Класс `Instant`

`Instant` - класс, который моделирует одну мгновенную точку на временной шкале (timestamp). Это может использоваться для
записи временных меток событий в приложении.

```java
class Main {
    public static void main(String[] args) {
        Instant time1 = Instant.now(); // 2019-12-14T15:38:29.033954Z
        Instant time2 = Instant.now(); // 2019-12-14T15:38:46.095633Z

        time1.isAfter(time2); // false
        time1.plus(3, ChronoUnit.DAYS); //  2019-12-17T15:38:29.033954Z
    }
}
```

### До java 8

До выхода Java 8 в распоряжении программиста имелись только три
класса, выполняющих за него большую часть этой работы. Класс `Date` инкапсулирует момент времени.
Класс `GregorianCalendar`, расширяющий абстрактный класс `Calendar`.

После Java 8 не рекомендуется их использовать. 