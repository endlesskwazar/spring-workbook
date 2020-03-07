# Spring Test

# Testing

# Refactoring

Юніт теести повинні бути невеликими і швидкими. Але використовуючи Spring DI, нам потрібно буде підняти інфраструктуру Spring для того щоб IoC і DI працював. Ідея в тому, що для юніт - тестування Spring взагалі не потрібен.

**Створення хороших spring beans для тестування**

Почнемо з поганого прикладу. Розглянемо наступний клас:

```java
@Service
public class RegisterUseCase {

  @Autowired
  private UserRepository userRepository;

  public User registerUser(User user) {
    return userRepository.save(user);
  }

}
```

Цей клас не може бути протестованим без Spring, тому що він не дає можливості передати екземпляр UserRepository. Для цього доводиться піднімати контекст Spring.  Урок тут - не використовувати впровадження залежностей через поля (field injection).

Натомість, ми можемо використати впровадженням залежностей через конструктор. Починаючи із версії Spring 4.3 анотації для впровадження залежностей через конструктор не потрібні. Але є кілька нюансів:
1. Конструктор повинен бути один
2. Якщо один конструктор присутній, а сетер позначений анотацією @Autowired, то обидва конструкторні та сетерні впровадження будуть виконані один за одним
3. З іншого боку, якщо взагалі немає @Autowire, то  об'єкт буде впроваджений один раз через конструктор, і сеттер можна використовувати звичайним способом без будь-яких ін'єкцій.

# Unit tests

# Functional tests

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