# Экспоненциальная форма

Необходимо реализовать класс числа в экспоненциальной форме с десятичным основанием.
Такое число состоит из двух компонент: мантиссы (significand) и экспоненты (exponent).
Например, число `12.345` представляется мантиссой `12345` и экспонентой `-3`.

Будем называть число в экспоненциальной форме _нормализованным_, если мантисса не делится на 10 или равна нулю.
В этом задании от вас требуется, чтобы все операции возвращали именно такие числа.

Интерфейс класса должен состоять из следующих операций:

- Конструирование без аргументов
- Конструирование от `int64_t`
- Конструирование от мантиссы и экспоненты (типа `int64_t`)
- Мантисса: `int64_t significand()`
- Экспонента: `int64_t exponent()`
- Явное приведение к `double`
- Перевод в строку: `std::string str()`
- Сложение: `+`, `+=`
- Вычитание: `-`, `-=`
- Умножение: `*`, `*=`
- Деление: `/`, `/=`
- Унарный минус: `-`
- Сравнение на равенство: `==`, `!=`
- Вывод в поток: `<<`

Обработка ошибок не требуется, однако операции стоит реализовывать так, чтобы минимизировать вероятность переполнения.

Допустимо добавление в публичный интерфейс дополнительных методов, если они семантически действительно должны быть
публичными.

За примерами использования можно обратиться к тестам к заданию.

# Арифметические выражения

Необходимо организовать иерархию классов для работы с вычислимыми арифметическими выражениями над типом `Exponential`.
Они должны быть хорошо вам знакомы по курсу программирования из первого семестра.

Виды выражений:

- `Const` (в конструкторе передаётся значение)
- `Variable` (в конструкторе передаётся имя переменной)
- `Negate` (унарный минус)
- `Add` (сложение)
- `Subtract` (вычитание)
- `Multiply` (умножение)
- `Divide` (деление)

Все эти классы должны (необязательно напрямую) наследоваться от `Expression`.

Пример конструирования выражения `2 * x + 1`:

```cpp
const Add expr(Multiply(Const(2), Variable("x")), Const(1));
```

Над выражениями должны быть реализованы соответствующие арифметические операторы.
Таким образом, предыдущий пример можно было бы записать так:

```cpp
const Add expr = Const(2) * Variable("x") + Const(1);
```

Аргументом методу `eval` передаётся отображение из имени переменной в её значение.
Он возвращает результат выражения, используя переданные значения вместо переменных.

```cpp
const Exponential result = expr.eval({
    {"x", Exponential(100)}
    {"y", Exponential(42)}
}); // 201
```

Вспомогательный метод `clone` должен возвращать указатель на такое же выражение, как то, на котором он вызван,
однако владение над указателем принадлежит вызвавшему метод.

Для класса `Expression` должен быть реализован оператор вывода в поток.

В этой части задания также не требуется обрабатывать ошибки.
