# Spring Core

${toc}

# Інверсія керування(IoC)

**Інверсія управління** (англ. Inversion of Control, IoC) - важливий принцип об'єктно-орієнтованого програмування, що використовується для зменшення зачеплення в комп'ютерних програмах. Також архітектурне рішення інтеграції, що спрощує розширення можливостей системи, при якому потік управління програми контролюється фреймворком.

методи реалізації:

- Шаблон «Фабрика» (англ. Factory pattern)
- Локатор служб (Service Locator)
- Впровадження залежності (англ. Dependency injection)

# Що таке Dependency injection?

Впровадження залежності (англ. Dependency injection, DI) — шаблон проектування програмного забезпечення, що передбачає надання зовнішньої залежності програмному компоненту, використовуючи «інверсію управління» (англ. Inversion of control, IoC) для розв'язання (отримання) залежностей.

Впровадження — це передача залежності (тобто, сервісу) залежному об'єкту (тобто, клієнту). Передавати залежності клієнту замість дозволити клієнту створити сервіс є фундаментальною вимогою до цього шаблону проектування.

## Приклад

Уявіть собі, що ми проектуємо систему в, якій кожного місяця потрібно виводити статистику на екран(статистику продаж тощо). Нехай цей об'єкт буди мати інтерфейс:

```java
public interface StatisticReporter {
	void report();
}
```

Все доволі просто, об'єкт буде мати один метод в інтерфейсі report(), який і виводить статистику на екран.

Користовуч може забажати мати статистику в різних форматах - HTML, XML, DOC. Для цих цілей ми введимо в системі інтерфейс:

```java
public interface Formatter {
	String format(String text);
}
```

І Зробимо декілька реалізації:

```java
public class HtmlFormatter implements Formatter {

	public String format(String text) {
		return "HTml format";
	}

}
```

```java
public class XMLFormatter implements Formatter {

	public String format(String text) {
		return "Xml format";
	}

}
```

І нерешті зробимо реалізацію StatisticReporter:

```java
public class StatisticReporterImpl implements StatisticReporter {
	
	HtmlFormatter formatter = new HtmlFormatter();
	
	public void report() {
		String report = "This is report";
		String outRep = formatter.format(report);
		System.out.print(outRep);
	}

}
```

Тестуємо систему:

```java
public class Main {
	
	public static void main(String[] args) {
		StatisticReporterImpl statisticReporterImpl = new StatisticReporterImpl();
		statisticReporterImpl.report();
	}
}
```

Якщо ми пішли таки шляхом, для того щоб виводити статистику в іншому форматы нам, або доведеться змінювати реалізацію statisticReporterImpl, або створювати ще один клас, який реалізує StatisticReporter.

Можна підти і іншим шляхом, замість того щоб створювати об'єкт Formatter всередині StatisticReporterImpl можна передати його ззовні:

```java
package test;

public class StatisticReporterImpl implements StatisticReporter {
	
	private Formatter formatter;
	
	public StatisticReporterImpl(Formatter formatter) {
		this.formatter = formatter;
	}
	
	public void report() {
		String report = "This is report";
		String outRep = formatter.format(report);
		System.out.print(outRep);
	}

}
```

```java
public class Main {
	
	public static void main(String[] args) {
		Formatter formatter = new HtmlFormatter();
		StatisticReporterImpl statisticReporterImpl = new StatisticReporterImpl(formatter);
		statisticReporterImpl.report();
	}
}
```

# Ще раз про IoC і DI

# Spring Core

# Створюємо проект і додаємо Spring Core

# Конфігурація впровадження, використовуючи XML

# Конфігурація впровадження, використовуючи Java

# Домашня робота

# Контрольні запитання

1. ваів
2. іваів
3. аіва
4. іва
5. іваі

