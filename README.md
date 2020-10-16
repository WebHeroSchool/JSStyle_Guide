# Руководство по стилю Java Script

---
## Оглавление

**1. Переменные**
**2. Строки**
**3. Функции**
**4. Форматирование**
**5. Инициализация массивов**
**6. Деструктуризация**
**7. Классы и конструкторы**
**8. Свойства**
**9. Комментарии**
**10. Пробел**
---

### 1. Переменные

#### Не используйте var
> Объявляйте все переменные с помощью const или let. Используйте const по умолчанию, если переменная не требует переназначения. Ключевое слово var не должно использоваться.
```
// bad
var example = 42;

// good
let example = 42;
```

#### Одна переменная за раз
> Каждое объявление локальной переменной объявляет только одну переменную.
```
// bad
let a = 1, b = 2, c = 3;

// good
let a = 1;
let b = 2;
let c = 3;
```

#### Константы
> Имена констант должны быть ЗАГЛАВНЫМИ_БУКВАМИ и через нижнее подчёркивание
```
// bad
const number = 5;

// good
const NUMBER = 5;
```

### 2. Cтроки
> Используйте шаблонные строки (разделённые символом `) вместо конкатенации комплексных строк, особенно если используется несколько строковых литералов. Шаблонные строки могут занимать несколько строк.
```
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
  return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

### 3. Функции
> Стрелочные функции делают синтаксис лаконичным и устраняют некоторые трудности с ним. Отдавайте предпочтение стрелочным функциям, вместо ключевого слова function, особенно для вложенных функций.
```
// bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```

### 4. Форматирование

#### Горизонтальное выравнивание
> Горизонтальное выравнивание не рекомендуется (но и не запрещается). Такая практика допустима, но, в целом, не рекомендуется. Не следует продолжать горизонтальное выравнивание даже в местах, где оно уже применялось.
```
// bad
{
  tiny:   42,  
  longer: 435, 
};

// good
{
  tiny: 42, 
  longer: 435,
};
```

#### Точки с запятыми
> Точки с запятыми обязательны. Каждое предложение должно отделяться точкой с запятой. Полагаться на автоматическую вставку точек с запятыми запрещается.
```
// bad
let luke = {}
let leia = {}
[luke, leia].forEach(jedi => jedi.father = 'vader')

// good
let luke = {};
let leia = {};
[luke, leia].forEach((jedi) => {
  jedi.father = 'vader';
});
```

#### Кавычки
> Используйте одинарные кавычки, а не двойные. Обычные строковые литералы разделяются одинарными кавычками (‘), а не двойными (“).
Совет: если строка содержит символ одинарной кавычки, попробуйте использовать шаблонные строки, чтобы не экранировать кавычки.
```
// bad
let directive = "No identification of self or mission."

// bad
let saying = 'Say it ain\u0027t so.';

// good
let directive = 'No identification of self or mission.';

// good
let saying = `Say it ain't so`;
```

### 5. Инициализация массивов
> Конструктор Array для объявления массивов использовать не рекомендуется.
```
// good
const a = []
const a = [1, 2, 3]
const a = Array.of(1, 2, 3)
const a = Array(6).fill(1) //инициализация каждого элемента массива, состоящего из 6 элементов, числом 1

// bad
const a = new Array() //не рекомендуется
const a = new Array(1, 2, 3) //не рекомендуется
```

### 6. Деструктуризация
> Используйте деструктуризацию объекта при доступе и использовании нескольких свойств объекта.
```
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}
```

### 7. Классы и конструкторы
> Всегда используйте class. Избегайте prototype.
```
// bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// good
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```

### 8. Свойства
> Используйте точечную запись при доступе к свойствам.
```
const luke = {
  jedi: true,
  age: 28,
};

// bad
const isJedi = luke['jedi'];

// good
const isJedi = luke.jedi;
```

### 9. Комментарии
> Используйте /** ... */для многострочных комментариев.
```
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
function make(tag) {

  // ...

  return element;
}

// good
/**
 * make() returns a new element
 * based on the passed-in tag name
 */
function make(tag) {

  // ...

  return element;
}
```

### 10. Пробел
> Используйте пробелы вместо табуляции. Помимо символа конца строки, символ горизонтального пробела ASCII (0x20), единственный разделитель, который следует использовать в любом месте исходного файла. Это означает, что символы табуляции не используются для отступов.Рекомендуется для отступа использовать два пробела (а не четыре).
```
// bad
function foo() {
∙∙∙∙let name;
}

// good
function baz() {
∙∙let name;
}
```

