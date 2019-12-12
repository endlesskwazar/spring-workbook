# Об'єкти. Класи. Базовий синтаксис класу

## Об'єкти. Класи

Java є об'єктно-орієнтованою мовою, тому такі поняття як "клас" і "об'єкт" грають в ньому ключову роль. Будь-яку програму на Java можна уявити як набір взаємодіючих між собою об'єктів.

Шаблоном або описом об'єкта є клас, а об'єкт являє екземпляр цього класу. Можна ще провести наступну аналогію. У нас у всіх є деяке уявлення про людину — наявність двох рук, двох ніг, голови, тулуба і т.д. Є деякий шаблон — цей шаблон можна назвати класом. Реально ж існуюча людина (фактично екземпляр даного класу) є об'єктом цього класу.

## Базовий синтаксис класу і його ініціалізація

Розгляньмо базовий синтаксис класу в java:

```java
[modifier] class [identiofier] [extends/implements] [..class, interface]{

	[identifier](){} //constructor (конструктор)

	{
		//динамічний ініціалізатор
	}

	static {
		// Статичний ініціалізатор
	}

	finilize(){} //destructor(деструктор)

	[modifier] [type] [name]; //property(атрибут)
	[modifier] [return_type] [identifier]([params]){ //method(метод)
		[some_code];
	}
}
```

Приклад:

```java
class Student {
	String name;
	
	Student(String name){
		this.name = name;
	}
	
	void printName() {
		System.out.println(this.name);
	}
}
```

Синтаксис створення об'єкта, використовуючи ключове слово new наступний:

```java
[type] [indentifier] = new([parameters for constructor]);

Student student = new Student("Alex");
```

## Getters/Setters

У кожного об'єкта є свої поля, згідно з принципом ООП поля класу треба оголошувати приватним модифікатором доступу. І отже, щоб змінювати та отримувати інформацію про поля об'єкта якраз і створюють геттери та сеттери з публічним доступом. Геттер видає значення поля викликає об'єкта, а сетер встановлює значення цього поля.

Зазвичай класи, які Ви будете писати виглядають наступним чином:

```java
class Student {
    private int age;
    
    public int getAge() {
        return this.age;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    private String name;
    
    public String getName() {
        return this.name;
    }
    
    public void String setName(String name) {
        this.name = name;
    }
}
```

Варто зауважити, що існує й інша точка зору на геттери та сеттери. Ось деякі недоліки використання геттерів і сеттерів:

- Об'єкт може бути розібраний по частинах іншими об'єктами, тому що вони в змозі вбудувати будь-які дані в об'єкт, через сеттери. Об'єкт просто не може приховати свій власний стан досить безпечно, тому що будь-хто може це стан змінити.
- Більшість програмістів вірять, що об'єкт — це структура даних з методами. Геттери та Сетери — не зло. Але більшість об'єктів, для яких створюються геттери та сеттери просто містять в собі дані. Це представлення викривляє ООП.

Детальніше можна прочитати [тут](https://www.javaworld.com/article/2073723/why-getter-and-setter-methods-are-evil.html)

## Java не підтримує перезавантаження операторів

Java не підтримує перезавантаження операторів — це вибір, який зробили його творці, які хотіли зробити мову простішою. Кожен оператор має хороший сенс завдяки арифметичній операції, яку виконує. Перевантаження оператора дозволяє зробити щось зайве, ніж те, на що очікується. Java дозволяє лише арифметичні операції на елементарних типах(+ String). Якщо ви дозволите розробнику робити перевантаження оператора, вони придумають декілька значень для одного оператора, що зробить криву навчання будь-якого розробника важкою, а речі ще більш заплутаними. Дизайнери Java хотіли завадити людям використовувати оператори в заплутаному вигляді.

# Методи класу Object

## toString()

**toString ()** надає рядкове представлення об'єкта і використовується для перетворення об'єкта в String. Метод toString () для класу Object повертає рядок, що складається з імені класу, об'єктом якого є екземпляр, символу '@ ' та шістнадцяткового зображення хеш-коду об'єкта. Іншими словами, він визначається як:

```java
public String toString()
{
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

Завжди рекомендується перевизначити метод toString(), щоб отримати власне рядкове — представлення об'єкта.

Наприклад, використовуючи атрибути класу:

```java
class Student {
	
	private int id;
	private String name;
	private int cardId;
	
	public Student(int id, String name, int cardId) {
		super();
		this.id = id;
		this.name = name;
		this.cardId = cardId;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getCardId() {
		return cardId;
	}

	public void setCardId(int cardId) {
		this.cardId = cardId;
	}

	@Override
	public String toString() {
		return "Student [id=" + id + ", name=" + name + ", cardId=" + cardId + "]";
	}
}
```

## hashCode()

Для кожного об'єкта JVM генерує унікальне число, яке називається хеш-кодом. Він повертає окремі цілі числа для різних об'єктів. Поширене помилкове уявлення про цей метод полягає в тому, що метод **hashCode ()** повертає адресу об'єкта, що є невірним. Він перетворює внутрішню адресу об'єкта в ціле число за допомогою алгоритму. Метод **hashCode ()** є нативні, тому що в Java неможливо знайти адресу об'єкта, тому він використовує рідні мови, такі як C/C ++, щоб знайти адресу об'єкта.

Використання методу **hashCode ()**: Повертає хеш-значення, яке використовується для пошуку об’єкта в колекції. JVM (Java Virtual Machine) використовує метод хеш-коду під час збереження об'єктів у хешованих структурах даних, таких як HashSet, HashMap, Hashtable тощо. Основна перевага збереження об'єктів на основі хеш-коду полягає в тому, що пошук стає простим.

> Примітка: Перевизначення методу hashCode () потрібно зробити таким чином, що для кожного об'єкта ми генеруємо унікальне число. Наприклад, для класу "Студент" ми можемо повернути номер залікової книги, оскільки він унікальний.

Приклад:

```java
class Student {
	private int cardNumber;
	
	public Student(int cardNumber) {
		this.cardNumber = cardNumber;
	}
	
	@Override
	public int hashCode() {
		return this.cardNumber;
	}
}
...
Student st = new Student(12);
System.out.println(st.hashCode());
...
```

![](../resources/img/2/7.png)

## equals(Object obj)

Порівняє переданий об’єкт із "this" об'єктом (об'єктом, щодо якого викликається метод). Це дає загальний спосіб порівняння об'єктів на рівність. Для отримання власної умови рівності потрібно перевизначити метод **equals (Object obj)**.

Стандартна реалізація:

```java
public boolean equals(Object obj) {
	return (this == obj);
}
```

Приклад перевизначення **equals()**:

```java
class Student {
	private int cardNumber;
	
	public int getCardNumber() {
		return this.cardNumber;
	}
	
	public Student(int cardNumber) {
		this.cardNumber = cardNumber;
	}
	
	@Override
	public boolean equals(Object obj) {
		if (this.cardNumber == ((Student)obj).getCardNumber())
			return true;
		return false;
	}
}
...
Student st1 = new Student(1);
Student st2 = new Student(1);
Student st3 = new Student(2);
System.out.println("st1 == st2 " + st1.equals(st2));
System.out.println("st1 == st3 " + st1.equals(st3));
...
```

![](../resources/img/2/8.png)

## getClass()

Повертає клас виконання об’єкта.

## finalize()

Цей метод викликається безпосередньо перед тим, як об’єкт буде знищено. Колектор сміття викликає його на об'єкті, коли збирач сміття визначає, що більше немає посилань на об'єкт.

## clone()

Метод clone() створює точну, "глибоку" копію об'єкта. Він створює новий екземпляр класу поточного об'єкта та ініціалізує всі його поля з точно вмістом відповідних полів цього об’єкта.

# Пакети

Пакети використовуються в Java для запобігання іменування конфліктів, контролю доступу, полегшення пошуку / розміщення та використання класів, інтерфейсів, перерахувань та приміток тощо.

Привила визначення пакетів:
- Імена пакетів записуються у нижньому регістрі, щоб уникнути конфлікту з іменами класів або інтерфейсів.
- Компанії використовують своє інвертоване доменне ім’я для початку імен пакунків, наприклад, com.example.mypackage для пакета з назвою mypackage, створеного програмістом на example.com.
- Пакети самою мовою Java починаються з java. або javax.

Синтаксис визначення пакету:

```java
package package_name;
//class definition code
```

> Визначення пакету повинно бути поміщено до будь-якого коду.

У деяких випадках ім'я домену в може бути не валідним пакетом. Це може статися, якщо доменне ім’я містить дефіс або інший спеціальний символ, якщо ім'я пакета починається з цифри чи іншого символу, який неможна використовувати як початок імені Java, або якщо ім'я пакета містить зарезервоване ключове слово Java, наприклад "int". У цьому випадку пропонується умова додати підкреслення. Наприклад:

|Невалідне|Валідне|
|-|-|
|hyphenated-name.example.org|org.example.hyphenated_name|
|example.int|int_.example|
|123name.example.com|com.example._123name|


## Імпортування класів

Для імпортування класів із пакетів використовується ключове слово import:

```java				
import [package].[class_name]; //Один клас із пакету
import [package].*; //Всі класи із пакету			
```

```java
import ua.edu.kdu.ius.Animal;

public class Main {

	public static void main(String[] args) {
		Animal animal = new Animal("Some name");
	}
}
```

## Статичне імпортування

В java також існує імпортування статичних методів і полів з інших класів:

```java
package ua.edu.kdu.ius;

public class Animal {

	private String name;

	public Animal(String name){
		this.name = name;
	}

	public void setName(String name){
		this.name = name;
	}

	public String getName(){
		return this.name;
	}

	public static void printAnimal(Animal animal){
		if(animal == null)
			return;
		System.out.println("Animal name: " + animal.name);
	}
}
```

```java
import ua.edu.kdu.ius.Animal;
import static ua.edu.kdu.ius.Animal.printAnimal;

public class Main {

	public static void main(String[] args) {
		Animal animal = new Animal("Some name");
		printAnimal(animal);
	}
}
```

# Три принципи ООП

## Інкапсуляція

Інкапсуляція — можливість приховування реалізації будь-яких частин модуля або об'єкта від зовнішнього світу (від клієнта). Це означає, що маніпулюючи модифікаторами доступу, можна приховати або відкрити тільки певні властивості, методи або класи для того, щоб непотрібні для класу-клієнта дані не були доступні.

Модифікатори доступу:

![](../resources/img/2/10.png)

## Наслідування

Наслідування дозволяє описати новий клас на основі вже існуючого (батьківського), при цьому властивості та функціональність батьківського класу запозичуються новим класом.

Для наслідування класу використовується ключове слово extends.

> Java не підтримує множинне наслідування.

Приклад:

```java
class Animal {
	private String name;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Animal(String name) {
		super();
		this.name = name;
	}
	
	
}

class Dog extends Animal {

	public Dog(String name) {
		super(name);
	}
	
}

...
Dog dog = new Dog("Sharik");
System.out.println(dog.getName());
...
```

![](../resources/img/2/9.png)

Доступ до батьківських полів і методів наступний:

![](../resources/img/2/10.png)

### Наслідування - зло?

Наслідування — це хороший механізм, але потрібно розуміти проблеми з якими можна стикнутися використовуючи цей принцип ООП де попало.

Річ у тому, що наслідування не враховує майбутні зміни батьківського класу. Адже коли ви успадковуєте новий клас від існуючого, ви підписуєте контракт про те, що новий клас завжди буде поводитися як існуючий, можливо розширюючи його поведінку в деяких місцях. У мовах програмування такий ефект спостерігається шляхом відсутності необхідності перевизначати публічні методи батьківського класу. А це означає, що їх з моменту успадкування можуть додати скільки завгодно і вам ніхто, включаючи компілятор, про це не скаже. А це, у свою чергу, може поламати вашу логіку успадкування з розширенням можливостей батьківського класу. Насправді варіанти є — написати модульний тест, який вважатиме кількість публічних і полу публічних методів і перевірить їх кількість. Це теж не дасть повної гарантії повідомлення, але вже краще. В ідеалі, варто було б при спадкуванні щоб уникнути сторонніх ефектів додавати тест, що фіксує сигнатури методів батьківського класу. Але хто це робить?

Це не всі мінуси успадкування. Коли у класу з'являється кілька спадкоємців, то у них є загальна поведінка, а є розширене. І часто доводиться морочитися з тестами, щоб уникнути дублікатів. Це вироджується в абстрактний тест, який кожен тест на дочірній клас повинен наслідувати. А що робити, якщо ви успадковуєте клас зі сторонньої бібліотеки. В цьому випадку потрібно писати тести на базову поведінку, дублюючи існуючі тести в бібліотеці? Або варто залишити їх як "надійні" без тестів?

В Java не можна розірвати спадкування стану від успадкування поведінки. Виходить, що якщо маєш бажання наслідувати стан (набір полів і дії над ними) ви змушені тягнути за собою і всю поведінку, що призводить до небажаних ефектів при майбутніх змінах. Можливо, наявність інших типів даних на зразок структур вирішило б цю проблему.

Практично будь-яке використання успадкування можна замінити на композицію. Для цього потрібен лише інтерфейс. Тестувати стає значно простіше, гнучкості стає більше, повідомлення про зміни буде давати компілятор, код стає менш пов'язаним. Одні переваги! Чому ж так не роблять на практиці? Відповідь проста — через лінь. Набагато простіше додати ще одного спадкоємця і дописати рядок коду, перекривши один з методів. Це вимагає менших зусиль.

**Про те як замінити наслідування композицією ми поговоримо пізніше.**

## Поліморфізм

**Поліморфізм** - це можливість застосування однойменних методів з однаковими або різними наборами параметрів в одному класі або в групі класів, пов'язаних відношенням наслідування.

Розгляньмо приклад. Допустимо в нас є об'єкт, який відповідальний за генерацію звіту. В ньому є метод report. Спочатку звіт повинен був генеруватися як просто текст. Далі функціональні вимоги змінилися і потрібно генерувати як текст так і xml. І можливо надалі формати будуть змінюватися.

Ось код, який вирішує поставлену задачу, використовуючи поліморфізм.

Визначимо базовий клас, який буде використовуватися для всіх класів, які будуть виступати як формат звіту.

```java
class ReportFormatter {
	public String format(String reportBody) {
		return reportBody;
	}
}
```

ReportFormatter містить всього один метод, в даному випадку він приймає звіт і повертає його ж. Створимо нащадка цього класу, перевизначивши метод format:

```java
class XMLReportFormatter extends ReportFormatter {
	@Override
	public String format(String reportBody) {
		return "<xml>" + reportBody + "</xml>";
	}
}
```

Створимо клас Report, який для цілей форматування звіту буде використовувати об'єкти типу ReportFormatter:

```java
class Report {
	private ReportFormatter formatter;
	
	public Report(ReportFormatter formatter) {
		this.formatter = formatter;
	}
	
	public String report() {
		String reportText = "Some report text";
		return this.formatter.format(reportText);
	}

}
```

Тепер для того, щоб створити звіт у форматі простого тексту нам достатньо створити екземпляр ReportFormatter і передати його в конструктор Report:

```java
	ReportFormatter formatter = new ReportFormatter();
	Report report = new Report(formatter);
	System.out.println(report.report());
```

![](../resources/img/2/2.png)


Відповідно, щоб отримати звіт у форматі xml, нам потрібно передати об'єкт типу XMLFormatter, оскільки він є нащадком ReportFormatter він може бути приведений до батьківського типу:

```java
ReportFormatter formatter = new XMLReportFormatter();
Report report = new Report(formatter);
System.out.println(report.report());
```

![](../resources/img/2/2.png)

А для того, щоб додати новий формат звіту до системи достатньо створити ще одного нащадка ReportFormatter:

```java
class HTMLReportFormatter extends ReportFormatter {
	@Override
	public String format(String reportBody) {
		return "<html>" + reportBody + "</html>";
	}
}

...
ReportFormatter formatter = new HTMLReportFormatter();
		Report report = new Report(formatter);
		System.out.println(report.report());
...
```

![](../resources/img/2/4.png)


### Ad-hoc polymorphism(method overloading)

Перевантаження методу — це функція, яка дозволяє класу мати більше одного методу, що має однакове ім'я, якщо їх аргументи списки різні. Перезавантаження також може бути застосоване до конструктора:

```java
class A {
	public A(int a) {
		System.out.println("Using constructor(int)");
	}
	
	public A(int a, int b) {
		System.out.println("Using constructor(int,int)");
	}
	
	public void sum(int a) {
		System.out.println("Using sum(int)");
	}
		
	public void sum(int a, int b) {
		System.out.println("Using sum(i		nt, int)");
	}
}	
...
A a = new A(3);
a.sum(5);
A a1 = new A(3,2);
a1.sum(5,4);
...
```		

![](../resources/img/2/5.png)


### Replace conditional with polymorphism

Такі конструкції як if, switch є елементами структурного програмування. Якщо ці конструкції зустрічаються у Вашому коді та створені для того, щоб виконувати рогалудження в залежності від типу об'єкта або його атрибутів можна застосувати такий прийом як "Replace conditional with polymorphism".

Розгляньмо наступний код:
```java
class SalesPerson {
	
	private int skill;
	public int getSkill() {
		return skill;
	}

	public void setSkill(int skill) {
		this.skill = skill;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	private String name;
	
	public SalesPerson(String name, int skill) {
		this.name = name;
		this.skill = skill;
	}
	
	public double evalAdditionalSalary() {
		if (skill >= 0 && skill <= 5)
			return 150d;
		else
			if (skill > 5 && skill <= 10)
				return 300d;
		return 500d;
	}
}
```

Метод getSkillTitle в залежності від цілочисельного параметра skill повертає його рядкове представлення. Змінімо наш код використовуючи "Replace conditional with polymorphism". Для цього:

- Створимо підкласи, яким відповідають відповідні гілки розгалуження.
- У підкласах створимо загальний метод і перенесіть відповідний код гілки з оригінального коду
- Замінимо умовний оператор викликом загального методу

```java
class SalesPerson {
	
	private int skill;
	public int getSkill() {
		return skill;
	}

	public void setSkill(int skill) {
		this.skill = skill;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	private String name;
	
	public SalesPerson(String name, int skill) {
		this.name = name;
		this.skill = skill;
	}
	
	public double evalAdditionalSalary() {
		throw new java.lang.UnsupportedOperationException("Not supported yet.");
	}
}

class Junior extends SalesPerson {

	public Junior(String name, int skill) {
		super(name, skill);
	}
	
	public double evalAdditionalSalary() {
		return 150d;
	}
	
}

class Middle extends SalesPerson {

	public Middle(String name, int skill) {
		super(name, skill);
	}
	
	public double evalAdditionalSalary() {
		return 300d;
	}
	
}

class Senior extends SalesPerson {

	public Senior(String name, int skill) {
		super(name, skill);
	}
	
	public double evalAdditionalSalary() {
		return 500d;
	}
	
}

public class Main {

	public static void main(String[] args) {
		SalesPerson s = new Middle("Alex", 8);
		System.out.println(s.evalAdditionalSalary());
	}

}
```

> Хоча у прикладі ми використали для батьківського класу звичайний метод, який вказує, що він не доступний, краще використовувати або абстрактні класи, або інтерфейси.

# Порядок ініціалізації класів

Зараз наше завдання полягає в тому, щоб дізнатися в якому порядку ініціалізуються статичні, динамічні властивості, відбуваються виклики конструкторів в ієрархії класів. Для цього розгляньмо наступний приклад:

```java
class A {
	protected int a;
	
	public A(int a) {
		this.a = a;
		System.out.println("Constructor Of A called");
	}
	
	{
		System.out.println("Dynamic init fo A called");
	}
	
	static {
		System.out.println("Static init for A called");
	}
}

class B extends A {
	protected int b;
	
	public B(int a, int b) {
		super(a);
		this.b = b;
		System.out.println("Constructor Of B called");
	}
	
	{
		System.out.println("Dynamic init fo B called");
	}
	
	static {
		System.out.println("Static init for B called");
	}
	
}

public class Main {

	public static void main(String[] args) throws InterruptedException {
		B b = new B(2,2);
	}

}
```

![](../resources/img/2/1.png)

З цього можна зробити висновок, що порядок ініціалізації класів наступний:

1. Статичні поля базового класу.
2. Статичний блок ініціалізації батьківського класу.
3. Статичні поля похідного класу.
4. Статичний блок ініціалізації похідного класу.
5. Поля базового класу.
6. Динамічний блок ініціалізації батьківського класу.
7. Конструктор базового класу.
8. Поля похідного класу.
9. Динамічний блок ініціалізації похідного класу.
10. Конструктор похідного класу.

# Абстрактні класи

Крім звичайних класів в Java є абстрактні класи. Абстрактний клас схожий на звичайний клас. В абстрактному класі також можна визначити поля і методи, водночас не можна створити об'єкт або екземпляр абстрактного класу. Абстрактні класи покликані надавати базовий функціонал для класів-спадкоємців. А похідні класи вже реалізують цей функціонал.

```java
abstract class Product {
	
}
```

Крім звичайних методів абстрактний клас може містити абстрактні методи. Такі методи визначаються за допомогою ключового слова abstract і не мають ніякого функціоналу:

```java
public abstract void display();
```

Розглянемо правила абстрактних класів:
- Абстрактний клас повинен оголошуватися, використовуючи ключове слово abstract
- Абстрактний клас може мати абстрактні та не абстрактні методи
- Неможливо створити екземпляр абстрактного класу
- Він може мати final - методи
- Може мати конструктор і статичні методи

![](../resources/img/2/6.png)

Приклад:

```java
abstract class Shape {
	public Shape() {}
	
	public abstract void draw();
}

class Rectangle extends Shape {
	public void draw() {
		System.out.println("Drawing rectangle");
	}
}
```

# Інтерфейси

Інтерфейс є типом — посиланням в Java. Вони схожі на абстрактні класи. Це сукупність абстрактних методів. Клас реалізує інтерфейс, тим самим успадковуючи абстрактні методи інтерфейсу.

Поряд з абстрактними методами інтерфейс може також містити константи, методи за замовчуванням, статичні методи та вкладені типи. Тіла методів існують лише для стандартних методів та статичних методів.

Приклад:

```java
interface Readable {
	void read(); //public void read
	static int GLOBAL_READ_FLAG = 0; //public final static int
	int LOCAL_READ_FLAG = 2;
	static void checkEnv() {
		System.out.println("Cheking env");
	}
	default void lock() {
		System.out.println("Trying to lock read");
	}
}
```

Описаний інтерфейс містить:
- публічний абстрактний метод read
- статичну константу
- локальну константу
- публічний статичний метод checkEnv
- стандартний метод lock

**Стандартні методи:**

До Java 8 інтерфейси могли мати лише абстрактні методи. Реалізація цих методів повинна забезпечуватися в окремому класі. Отже, якщо новий метод потрібно додати в інтерфейс, код його реалізації повинен бути наданий у класі, що реалізує той самий інтерфейс. Щоб подолати цю проблему, Java 8 представила концепцію методів за замовчуванням, які дозволяють інтерфейсам мати методи з реалізацією, не впливаючи на класи, які реалізують інтерфейс.

> На відмінну від наслідування, коли один клас може бути наслідуваний від одного єдиного класу, клас може реалізувати безліч інтерфейсів.


## Поліморфізм, використовуючи інтерфейси

Перепишімо приклад із розділу про поліморфізм використовуючи інтерфейси. Тепер базовий клас ReportFormatter стає інтерфейсом:

```java
interface ReportFormatter {
	String format(String reportBody);
}

class XMLReportFormatter implements ReportFormatter {

	@Override
	public String format(String reportBody) {
		return "<xml>" + reportBody + "</xml>";
	}
	
}

class Report {
	private ReportFormatter formatter;
	
	public Report(ReportFormatter formatter) {
		this.formatter = formatter;
	}
	
	public String report() {
		String reportText = "Some report text";
		return this.formatter.format(reportText);
	}

}
...
ReportFormatter formatter = new XMLReportFormatter();
Report report = new Report(formatter);
System.out.println(report.report());
...
```

![](../resources/img/2/11.png)

# Заміна наслідування композицією

Припустимо, що в нас є клас, який може прочитати файл з диску і повернути його контент:

```java
class Read {
	
	private String fileName;

	public String getFileName() {
		return fileName;
	}

	public void setFileName(String fileName) {
		this.fileName = fileName;
	}

	public Read(String fileName) {
		super();
		this.fileName = fileName;
	}
	
	public String read() {
		return "Content of file";
	}
	
}
```

Нам потрібно створити ще один клас ConfigFile, який також може прочитати контент з файлу. Замість того, щоб наслідувати клас File, ми можемо створити поле в класі FileConfig і делегувати виконання читання:

```java
class ConfigFile {
	
	private File file;

	public ConfigFile(File file) {
		super();
		this.file = file;
	}
	
	public String getConfigContent() {
		return this.file.read();
	}
}
...
ConfigFile cf = new ConfigFile(new File("text.txt"));
System.out.println(cf.getConfigContent());
...
```

![](../resources/img/2/13.png)

# Enum

Enum - це особливий тип даних, який дозволяє змінній бути набором заздалегідь визначених констант. Змінна повинна дорівнювати одному із попередньо визначених для неї значень. Найпоширеніші приклади включають напрямки компаса (значення Північного, Південного, Східного та Західного) та дні тижня.

Оскільки enum містить константи, назви полів типу enum пишуться великими літерами.

```java
enum Day {
	SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
	THURSDAY, FRIDAY, SATURDAY 
}

public class Main {
	Day day;
	
	public Main(Day day) {
		this.day = day;
	}
	
	public void tellItLikeItIs() {
		switch (day) {
			case MONDAY:
				System.out.println("Mondays are bad.");
				break;
					
			case FRIDAY:
				System.out.println("Fridays are better.");
				break;
						 
			case SATURDAY: case SUNDAY:
				System.out.println("Weekends are best.");
				break;
						
			default:
				System.out.println("Midweek days are so-so.");
				break;
		}
	}
	
	public static void main(String[] args) {
		Main firstDay = new Main(Day.MONDAY);
		firstDay.tellItLikeItIs();
		Main thirdDay = new Main(Day.WEDNESDAY);
		thirdDay.tellItLikeItIs();
		Main fifthDay = new Main(Day.FRIDAY);
		fifthDay.tellItLikeItIs();
		Main sixthDay = new Main(Day.SATURDAY);
		sixthDay.tellItLikeItIs();
		Main seventhDay = new Main(Day.SUNDAY);
		seventhDay.tellItLikeItIs();
	}
}
```

![](../resources/img/2/12.png)

# Скільки пам'яті займають об'єкти

В java - everything is an object. Крім, мабуть, примітивів і посилань на самі об'єкти. Розгляньмо дві типові ситуації:

```java
int a = 300;
Integer b = 301;
```

У цих простих рядках різниця просто величезна, як для JVM так і для ООП. У першому випадку, все що у нас є — це 4-х байтна змінна, яка містить значення зі стека. У другому випадку у нас є змінна посилання і сам об'єкт, на який ця змінна посилається. Отже, якщо в першому випадку ми знаємо, що розмір змінної рівний:

```java
sizeOf(int)
```

То у другому випадку:

```java
sizeOf(reference) + sizeOf(Integer)
```

**Щоб дізнатися скільки займає об'єкт розгляньмо з чого він складається:**

- Заголовок об'єкта
- Пам'ять для примітивних типів
- Пам'ять для змінних посилань
- Зміщення / вирівнювання (по суті, це кілька невикористовуваних байтів, що розміщуються після даних самого об'єкта. Це зроблено для того, щоб адреса в пам'яті завжди була кратному машинному слову, для прискорення читання з пам'яті + зменшення кількості біт для покажчика на об'єкт + імовірно для зменшення фрагментації пам'яті. Варто також відзначити, що в java розмір будь-якого об'єкта кратний 8 байтам!)

**Розгляньмо детальніше структуру заголовка об'єкта.**

Кожен екземпляр класу містить заголовок. Кожен заголовок для більшості JVM (Hotspot, openJVM) складається з двох машинних слів. Якщо мова йде про 32-х розрядну систему, то розмір заголовка - 8 байтів, якщо мова про 64-х розрядну систему, то відповідно - 16 байтів. Кожен заголовок може містити наступну інформацію:
- Маркувальне слово (mark word) - Використовується збирачем сміття і HotSpot для ефективного блокування.
- Hash Code - кожен об'єкт має хеш код. За замовчуванням результат виклику методу Object.hashCode () поверне адресу об'єкта в пам'яті, проте деякі збирачі сміття можуть переміщувати об'єкти в пам'яті, але хеш код завжди залишається одним і тим же, через те, що місце в заголовку об'єкта якраз може бути використано для зберігання оригінального значення хеш коду.
- Garbage Collection Information - кожен java об'єкт містить інформацію потрібну для системи управління пам'яттю. Найчастіше це один або два (біта-прапора), але також це може бути, наприклад, якась комбінація бітів для зберігання кількості посилань на об'єкт.
- Type Information Block Pointer - містить інформацію про тип об'єкта. Цей блок включає інформацію про таблиці віртуальних методів, покажчик на об'єкт, який представляє тип і покажчики на деякі додаткові структури, для більш ефективних викликів інтерфейсів і динамічної перевірки типів.
- Lock - кожен об'єкт містить інформацію про стан блокування. Це може бути покажчик на об'єкт блокування або пряме уявлення блокування.
- Array Length - якщо об'єкт — масив, то заголовок розширюється 4 байтами для зберігання довжини масиву.

**Розмір посилань.**

В принципі, розмір посилання у JVM залежить від її розрядності. Тому в 32-х розрядних JVM розмір посилання зазвичай 4 байти, а в 64-х розрядних - 8 байтів. Хоча ця умова і не обов'язкова.

**Беручи до уваги всю цю інформацію, спробуймо приблизно розрахувати розмір об'єкта**

Розраховувати розмір ми будемо для наступного класу:

```java
class MyInt {
	private int value;
	
	public int getValue() {
		return value;
	}

	public void setValue(int value) {
		this.value = value;
	}

	public MyInt(int value) {
		this.value = value;
	}
}
```

Ітак, розмір об'єкта рівний:

```java
sizeOf(reference) + sizeOf(MyInt)
```

Припустимо, що наш код буде виконуватися на 64-х бітній платформі, тоді sizeOf(reference) - 8 байтів. Тепер нам потрібно розрахувати sizeOf(MyInt), це доволі просто, кожен об'єкт містить заголовок, беручи до уваги розрядність це буде 16 байтів. Наш клас містить всього-на-всього одне примітивне поле, це ще 4 байти. Складаємо докупи: 8 + 16 + 4 = 28 байтів.

> Disclaimer. Розрахований розмір не є точним, на нього можуть впливати багато факторів.

# Домашня робота

Завантажте [Eclipse](https://www.eclipse.org/downloads/). Створіть новий Java додаток, виконайте всі варіанти.

## Варіанти

1. Створіть клас Enemy(health, dmg, type). Створіть метод у класі Enemy - attack, який наносить dmg + бонусний урон в залежності від типу. Переробіть завдання, використовуючи "replace conditional with polymorphism".
2. Створіть клас VideConverter, який в залежності від інших об'єктів(які реалізують інтерфейс Encoder) конвертують відео в різні формати.(Дійсну логіку конвертування імплементить не потрібно).
3. Є наступний код:
```java
class UseCompact {
	
	private double value;
	
	public UseCompact(double value) {
		super();
		this.value = value;
	}

	public double useCompact() {
		return this.value;
	}
}

class DoubleBox {
	private double value;
	public DoubleBox(double value, int presicion, UseCompact useCompact) {
		super();
		this.value = value;
		this.presicion = presicion;
		this.useCompact = useCompact;
	}
	private int presicion;
	private UseCompact useCompact;
	public double getValue() {
		return value;
	}
	public void setValue(double value) {
		this.value = value;
	}
	public int getPresicion() {
		return presicion;
	}
	public void setPresicion(int presicion) {
		this.presicion = presicion;
	}
	
}
```

Розрахуйте, скільки, приблизно буде займати об'єкт DoubleBox, розпишіть логіка розрахунку.

# Контрольні запитання

1. Поясніть терміни "клас" і об'єкт.
2. Що таке геттери та сеттери? Які ви знаєте недоліки використання геттерів і сеттерів?
3. Назвіть методи класу Object.
4. Що таке пакети в java?
4. Поясніть принципи наслідування, інкапсуляція і наслідування.
5. Що таке абстрактні класи?
6. Що таке інтерфейси? Що можуть містити інтерфейси?
7. Як порахувати, скільки займатиме об'єкт в java?