## Използване на обектите и свойствата им

Всичко в JavaScript действа като обект. Има само две изключения: 
[`null`](#core.undefined) и [`undefined`](#core.undefined).

    false.toString(); // 'false'
    [1, 2, 3].toString(); // '1,2,3'
    
    function Foo(){}
    Foo.bar = 1;
    Foo.bar; // 1

Често срещано погрешно схващане е, че числата не могат да бъдат използвани
като обекти. Това се случва поради пропуск в синтактичния анализатор на
JavaScript, който разбира точката като десетична запетая.

    2.toString(); // в браузър хвърля синтактична грешка (SyntaxError)

Има три начина да се накарат буквално изписаните числа в програмния код също
да действат като обекти.

    2..toString(); // втората точка е разпозната правилно
    2 .toString(); // забележете оставеното място пред точката
    (2).toString(); // първо се изчислява изразът между скобите

### Обектите като тип данни

Обектите в JavaScript могат също да бъдат използвани като [*Хеш-таблици*][1].
Те се състоят от именувани полета, сочещи към някакви стойности.

Обект може да се създаде като се използва буквално представяне. Новият обект
[наследява](#object.prototype) от `Object.prototype` и няма [собствени
полета](#object.hasownproperty).

    var foo = {}; // нов празен обект

    // нов обект с поле 'test', което има стойност 12
    var bar = {test: 12}; 

### Достъп до полета

Полетата (свойства) на даден обект могат да се ползват, като се използва точка
(обект.именаполе) или чрез използване на квадратни скоби (обект['именаполе']).
    
    var foo = {name: 'kitten'}
    foo.name; // kitten
    foo['name']; // kitten
    
    var get = 'name';
    foo[get]; // kitten
    
    foo.1234; // SyntaxError
    foo['1234']; // работи

Двата вида изписване работят по един и същи начин с единствената разлика, че
когато използваме квадратни скоби, можем динамично да създаваме нови полета и
да ползваме идентификатори, които иначе биха довели до синтактична грешка.

### Изтриване на полета

Единственият начин да се изтрие поле е като се използва операторът `delete`.
Задаване на стойност `undefined` или `null` само премахва *стойността* на
полето, но не и самото него -- *ключа*.

    var obj = {
        bar: 1,
        foo: 2,
        baz: 3
    };
    obj.bar = undefined;
    obj.foo = null;
    delete obj.baz;

    for(var i in obj) {
        if (obj.hasOwnProperty(i)) {
            console.log(i, '' + obj[i]);
        }
    }

Кодът горе показва `bar undefined` и `foo null` - само полето `baz`  е
изтрито и го няма в изхода на скрипта.

### Изписване на ключове

    var test = {
        'case': '"case" е ключова дума, затова трябва да бъде оградена с кавички',
        delete: '"delete" също' // хвърля SyntaxError
    };

Свойствата (полетата) на обектите може да се изписват като обикновени низове в
кавички или направо (без кавички). Поради друг пропуск в анализатора на
JavaScript, горният код хвърля `SyntaxError` преди ECMAScript 5.

Тази грешка се получава, тъй като `delete` е *ключова дума*. В такива случаи
полетата трябва да се изписват в кавички при ползване на по-стар JavaScript
двигател.

[1]: https://bg.wikipedia.org/wiki/Хеш-таблица

