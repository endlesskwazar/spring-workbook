# Cookie, Session

## Cookie

### Встановлення cookie і читання cookie

Щоб встановити cookie у Spring Boot, ми можемо використовувати метод addCookie() класу HttpServletResponse. Все, що вам потрібно зробити - це створити новий екземпляр класу Cookie і додати його до відповіді.

```java
@GetMapping("/setCookie")
@ResponseBody
public String setCokkie(HttpServletResponse response) {
	Cookie cookie = new Cookie("username", "exndlesskwazar");
	response.addCookie(cookie);
	return "Cookie was set";
}
```

Щоб прочитати cookie можна використати метод getCookies() класу HttpServletRequest.

```java
@GetMapping("/getCookie")
@ResponseBody
public String getCookie(HttpServletRequest request) {
	Cookie[] cookies = request.getCookies();
	if (cookies != null) {
		return Arrays.stream(cookies)
				.map(c -> c.getName() + "=" + c.getValue()).collect(Collectors.joining(", "));
	}
	return "No cookies";
}
```

![](../resources/img/cookie,session/1.png)

![](../resources/img/cookie,session/2.png)

![](../resources/img/cookie,session/3.png)

В Spring є ще один спосіб прочитати cookie - використовуючи анотацію @CookieValue:

```java
@GetMapping("/getOneCookie")
@ResponseBody
public String getOneCookie(@CookieValue(value = "username", defaultValue="anonymus") String username) {
	return "username " + username;
}
```

defaultValue - якщо cookie не встановлений використовується

Також в CookieValue є ще один корисний атрибут requred, який за відстуності встановленого cookie викине org.springframework.web.bind.MissingRequestCookieException:

```java
@GetMapping("/getOneCookie")
@ResponseBody
public String getOneCookie(@CookieValue(value = "username", required = true) String username) {
	return "username " + username;
}
```

Якщо час життя cookie не вказаний, він триває доти, доки сеанс не закінчиться. Такі файли cookie називаються сесійними файлами cookie. Файли cookie сесії залишаються активними, поки користувач не закриє веб-переглядач або не очистить файли cookie. Файл cookie користувача, створений вище, насправді є файлом cookie сеансу.

Але ви можете змінити цю поведінку за замовчуванням і встановити час закінчення файлу cookie, використовуючи метод setMaxAge () класу Cookie.

```java
Cookie cookie = new Cookie("username", "endlesskwazar");
cookie.setMaxAge(7 * 24 * 60 * 60); // expires in 7 days
```

### Secure cookie

Захищеним cookie є той, який надсилається серверу лише через зашифроване з'єднання HTTPS. Захищені файли cookie не можуть передаватися серверу через незашифровані HTTP-з'єднання.

```java
Cookie cookie = new Cookie("username", "endlesskwazar");
cookie.setMaxAge(7 * 24 * 60 * 60); // expires in 7 days
cookie.setSecure(true);
```

### HttpOnly Cookie

Файли cookie HttpOnly використовуються для запобігання атак міжсайтових скриптів (XSS) та не доступні через API Document.cookie JavaScript API. Коли для файлу cookie встановлено прапор HttpOnly, він повідомляє браузеру, що цей певний файл cookie має бути доступним лише сервером.

```java
Cookie cookie = new Cookie("username", "Jovan");
cookie.setMaxAge(7 * 24 * 60 * 60); // expires in 7 days
cookie.setSecure(true);
cookie.setHttpOnly(true)
```

### Cookie Scope

Якщо область не вказана, cookie надсилається серверу лише для шляху, який був використаний для його встановлення у браузері. Ми можемо змінити цю поведінку, використовуючи метод setPath() класу Cookie. Це встановлює директиву Path для файлу cookie.

```java
Cookie cookie = new Cookie("username", "endlesskwazar");
cookie.setMaxAge(7 * 24 * 60 * 60); // expires in 7 days
cookie.setSecure(true);
cookie.setHttpOnly(true);
cookie.setPath("/"); // global cookie accessible every where
```

### Видалення Cookie

Щоб видалити файл cookie, встановіть директиву Max-Age на 0 та скасуйте її значення. Ви також повинні передати ті самі інші файли cookie, які ви використовували для встановлення. Не встановлюйте значення директиви Max-Age на -1. В іншому випадку браузер буде розглядатись як cookie сеансу.

```java
Cookie cookie = new Cookie("username", null);
cookie.setMaxAge(0);
cookie.setSecure(true);
cookie.setHttpOnly(true);
cookie.setPath("/")
```

## Session

## Повідомлення про успішну операцію

# Домашнє завдання

Запропонуйте власну реалізацію динамічного масиву, який заснований на звичайномк масивові. Інтерфейс - add(elem), remove(elem), remove(index), get(index), isExists(elem).

# Контрольні запитання

1. Що таке cookie?
2. Як в Spring встановити cookie?
3. Поясніть параметри Secure cookie, HttpOnly Cookie, Cookie Scope.
4. Як в Spring прочитати всі cookie?
5. Поясніть анотацію CookieValue і її параметри defaultValue, required.