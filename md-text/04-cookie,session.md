# JDBC TEmplates

# Application profiles

Spring Boot застосовує свою типову умову щодо підходу до налаштування. Це означає, що ми можемо просто помістити файл «application.properties» у каталог «src/main/resources», і він буде автоматично виявлений. Тоді ми можемо зчитувати з нього будь-які завантажені властивості.

Додаймо у файл application.properties властивість:

application.properties:
```
myprop=myprop value
```

Зчитати цю властивість можна наступними способами:

1. Отримати із контексту клас Environment і викликати метод getProperty()

```java
...
@Autowired
private Environment env;
...
System.out.println(env.getProperty("myprop"));
...
```

2. Використати анотацію @Value

```java
...
@Value("${myprop}")
private String myProp;
...
System.out.println(this.myProp);
...
```

> Назви властивостей можуть мати крапки у своїх іменах.
> 
> application.properties можуть містити властивісті, які визначені користувачем, так і властивості, які вбудовані і предназначені для конфігурації Spring. Подивитися список визначених властей можна [тут](https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html).

# Spring profiles

Spring надає могутній інструмент для групування конфігураційних властивостей у так звані профілі, що дозволяє нам активувати купу конфігурацій з одним параметром профілю. Spring Boot спирається на це, дозволяючи нам налаштувати та активувати профілі зовні.

Профілі ідеально підходять для налаштування нашої програми для різних середовищ, але вони спокушають і в інших випадках використання.

Активація певного профілю може мати величезний вплив на додаток Spring Boot, але під капотом профіль може просто керувати двома речами:

- профіль може впливати на властивості програми
- профіль може впливати на те, які компоненти завантажуються в контекст програми.

Приклад:

Як стартовий проект використаємо [shop-basic-mvc](https://github.com/endlesskwazar/spring-examples/tree/shop-basic-mvc)

Додамо файд application-jdbc.properties в src/main/resources.

application.properties:
```
myprop=myprop value
spring.profiles.active=jdbc
```

application-jdbc.properties:
```
myprop=my prop jdbc value
```

Як результати ми отримаємо значення myprop = my prop jdbc value. Якщо ми видалимо строчку spring.profiles.active=jdbc, то значення myprop = myprop value.

Для створення і активації профілю потрібно:
- Створити файл application-[profile_name].properties. Всі значення, які цей файл визначає будуть перезаписані поверх application.properties
- Активувати профіль в application.properties за допомогою вказання атрибута spring.profiles.active=[profile-name]

Додаймо до проекту ще одну реалізацію інтерфейсу Repository для роботи із продуктами:

ProductRepositoryJdbc:
```java
@Repository
public class ProductRepositoryJdbc implements com.example.demo.repository.Repository<Product, Long> {

	@Override
	public Product save(Product entity) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public Optional<Product> getById(Long id) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public Iterable<Product> findAll() {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public void removeById(Long id) {
		// TODO Auto-generated method stub
		
	}

}
```

Тепер в нас ж два компоненти, які можуть бути використані в ProductService, а саме:
- ProductRepository
- ProductRepositoryJdbc

Щоб використати саме ProductRepositoryJdbc додамо анотацію Profile:

```java
@Repository
@Profile("jdbc")
public class ProductRepositoryJdbc implements com.example.demo.repository.Repository<Product, Long> {
```

Для ProductRepository також встановимо свій профіль:

```java
@Repository
@Profile("dummy-data")
public class ProductRepository implements com.example.demo.repository.Repository<Product, Long> {
```

# JDBC Templates

## З'єднання із базою даних

## Додавання тестових даних. CommandLineRunner

## Отримати список

## Деталі

## Додавання

## Видалення

# Домашнє завдання

Запропонуйте власну реалізацію динамічного масиву, який заснований на звичайномк масивові. Інтерфейс - add(elem), remove(elem), remove(index), get(index), isExists(elem).

# Контрольні запитання

1. Що таке Generics і навіщо вони потрібні?
2. Що таке Java Collection Framework?
3. Перелічіть інтерфейси Java Collection Map.
4. Поясніть колекції - Hashtable, HashMap, LinkedHashMap, TreeMap.
4. Поясніть колекції - Vector, Stack, ArrayList, LinkedList.
4. Поясніть колекції - HashSet, LinkedHashSet, TreeSet.
4. Поясніть колекції - PriorityQueue, ArrayDeque.
4. Як вибрати, яку колекцію використовувати?