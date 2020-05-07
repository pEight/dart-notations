# Dart Lang

Dart é uma linguagem mmultiparadigma desenvolvida pela google. Na linguagem, tudo que pode ser passado para uma variável é 
um objeto e todo objeto se origina de uma classe. Isso significa que valores do tipo Int, Boolean, String, etc são objetos e surgem 
a partir de uma classe. Além disso, dart possui expressões e declarações. Enquanto expressões retorna algum valor em tempo de
execução, uma declaração em Dart não faz isso. Oserva-se que uma declaração pode ter n expressões enquanto uma expressão não pode ter
uma declaração.

## Variaveis

Uma váriavel é um recurso que armazena uma referência para um objeto em memória. Declaramos uma váriavel da seguinte forma:

```dart
var foo = 'Some String'
```

A linguagem infere o tipo da variável e portanto não precisamo informá-lo e assim utilizamos a palavra-chave `var`. Se for optado
por explicitar o tipo, é preciso substituir `var` pelo tipo em questão.

```dart
String foo = 'Some String';
```

Não passando nenhum valor para uma váriavel faz com que seu valor inicial seja `null`. Para tornar uma variável imutavel,
troca-se `var` por `final` ou `const`. Uma variável `final` pode receber um valor uma única vez em seu tempo de vida.
Uma `const` variável são constantes de tempo de compilação. Uma `const` é um `final` mas o contrário não é válido.

```dart
final foo = 'Some Final String';

final Int baz = 7;
```

## Tipos

- Number(Dividido em int e double)
- String
- Boolean
- Lists
- Sets
- Maps
- Runes
- Symbols


```dart
// Number
num a = 1.2
int b = 1
double c = 2.1

// String
String str = 'Some String';

// Boolean
bool isApple = false;

// Lists
List l = [1, 2, 3, 4, 5, 6, 7];

// Sets
Set s = { 1, 2 };
s.add(3);
s.addAll(4, 5, 6);

// Maps
Map m1 = {
  'one': 1,
  'two': 2,
  'three': 3,
  'four': 4,
}

Map m2 = {
  0: 'one',
  1: 'two',
  2: 'three',
  3: 'four',
}
```

**Algumas observações**: 

- Em listas temos o spread operator(`...`). Caso não se tenha certeza sobre o valor a direita
do spread operator, tem-se o null-aware spread operator(`?...`)

- Em Maps, uma chave que não tem valor definido tem como valor inicial `null`.

## Funções

Como foi mencionado acima, praticamente tudo é um objeto em Dart. E função portanto é um objeto. Uma função pode ser declarada de
duas formas e tanto em top-level como em class-level.

```dart
String hello(String name) {
  return 'Hello, $name';
}

String shortHello(String name) => 'Hello, $name';
```

Uma função pode ter dois tipos de parametros: Obrigatórios e Opcionais. Os obrigatórios sempre devem ser listados primeiros. Além disso,
Os parametros opcionais são `named` ou `positional`.

```dart
// named parameters
  String getCompleteName(String firstname, { String middlename, String lastname }) {
    return '$firstname ${middlename??''} $lastname';
  }

getCompleteName('Phillipe', lastname: 'Queiroz'); // 'Phillipe Queiroz'
```

Um parametro named pode ser definido como obrigatório adicionando `@required`.
```dart
// named parameters
  String getCompleteName(String firstname, { String middlename, @required String lastname }) {
    return '$firstname ${middlename??''} $lastname';
  }

getCompleteName('Phillipe', lastname: 'Queiroz'); // 'Phillipe Queiroz'
```

```dart
String getCompleteName(String firstname, [String middlename = '', String lastname = '']) {
  return '$firstname $middlename $lastname';
}

getCompleteName('Phillipe', 'César'); // 'Phillipe César'
```

Na função mostrada acima, foi definido valores padrões para middlename e lastname caso não seja passado nenhum valor.

Uma função em dart é de primeira classe. Portanto ela pode ser passada como argumento para outra função e ser passada para uma
variável.

```dart
var getCompleteName = (String firstname, { String middlename = '', String lastname = '' }) => '$firstname $middlename $lastname';
```

Todos os exemplos dados, é declaro o tipo de retorno da função. Essa informação pode ser omitida já que Dart infere tipos. Logo:

```dart
getCompleteName(String firstname, { String middlename = '', String lastname = '' }) {
  return '$firstname $middlename $lastname';
}
```

Mas também é possível criar funções anônimas. Assim podemos ter isso:

```dart
(String firstname, { String middlename = '', String lastname = '' }) {
  return '$firstname $middlename $lastname';
}
```

Por fim, como funções são de primeira classe, é posivel também fazer o seguinte:

```dart
var getCompleteName = (String firstname, { String middlename = '', String lastname = '' }) {
  return '$firstname $middlename $lastname';
};
```
