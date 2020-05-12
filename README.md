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

Suponha duas funções em Dart f e g. A função g é declarada dentro do corpo da função f. O primeiro comportamento que podemos tirar
baseado nessa estrutura é que g só é reconhecida dentro de g e portanto não pode ser chamada fora do corpo da função f. O segundo
comportamento é que g tem acesso as variáveis de f. Isso se aplica a um nível de aninhamento maior. Ou seja, a função mais interna
tem acesso as variáveis das funções externas. A isso chamamos de lexical scope.

Uma **closure** é uma função que tem acesso as variáveis no lexical scope, mesmo sendo usada fora do escopo original. Por exemplo, sabe-se
que uma função pode retornar uma função:

```dart

Function makeAdd(num a) {
  const c = 1;

  return (num b) => a + b + c;
}

const add = makeAdd(2);

add(3) // 2 + 3 + 1 = 6
```

A função retornada `(num b) => a + b + c` é uma closure.

## Classes

Sabe-se que tudo em Dart é um objeto e que todo objeto é moldado por uma classe. Diferente de Java, Dart possui uma herança baseada 
em mixin. Todas as classes com exceção de Object possui uma super classe, porém o corpo de uma classe pode ser reutilizado através de
mesclagem de classes.

Um objeto possui membros que representam comportamentos(funções, métodos) ou caracteristicas(variáveis, atributos).

```dart

const p1 = Point(1, 1);

p1.x; // 1
p1.y; // 1

p1.printCoords(); // (1, 1)
```

**Observação**: Caso não se tenha certeza do valor do operando mais a esquerda, utiliza-se `?.` ao inves de `.`

```dart

const swCharacter;

swCharacter.name = 'Han Solo' // ERROR

swCharacter?.name = 'Han Solo' // Se swCharacter for não nulo, atribuir ao seu atributo name o valor 'Han Solo' 
```

Um conceito comum em linguagens orientadas a objeto são o de construtores. Construtor é uma função responsável por inicializar um objeto.
Em Dart existem construtores da forma `ClassName` e `ClassName.namedConstructor`.

```dart

const p1 = Point(2, 1);
const pOrigin = Point.source(); // x = 0 e y = 0
```

Cria-se uma classe utilizando a palavra-chave `class`.

```dart

class Point {
  // INSTANCE VARIABLES. All initialized with null value
  num x; 
  num y;


  // CONSTRUCTORS
  // Without suggar syntax
  Point(x, y) {
    this.x = x;
    this.y = y;
  }

  // With suggar syntax
  Point(this.x, this.y);
}
```

Se uma variável de instância receber alguma informação na classe, o valor é atribuido quando um objeto da classe for instânciado.

```dart

import 'dart:math';

class Point {
  num x = 0;
  num y = 0;
  
  Point();
  
  Point.twoDimentional(dx, dy) {
    x = dx;
    y = dy;
  }
  
  double distanceTo(Point p1) {
    var xPart =  p1.x - x;
    var yPart = p1.y - y;
  
    return sqrt( pow(xPart, 2) + pow(yPart, 2) );
  }
}

main() {
  var p1 = Point();
  
  print(p1.x); // 0
  print(p1.y); // 0
}
```

**Observação**: a palavra-chave `this` deve ser utilizada apenas quando ocorre conflito de nomes.

**Observação**: Se não for declarado um construtor, um construtor padrão sem argumentos é fornecido. O construtor
padrão invoca o construtor padrão da superclasse. Além disso, construtores não são herdados, mas podem ser invocados na
subclasse.

O construtor em uma subclasse chama em seu corpo o construtor sem nome e sem argumentos da superclasse por padrão. Caso seja usado
uma lista de inicialização, a ordem de chamada ocorre da seguinte forma:

1. Lista de inicialização.
2. Construtor sem nome e sem argumento da superclasse.
3. Construtor principal da classe principal.

Veja que esse comportamento pode mudar. É possível definir o construtor do passo 2 da list acima.

```dart

class Point2D {
  num x;
  num y;
   
  Point2D(this.x, this.y);
  
  Point2D.fromJson(Map<String, num> point) {
    x = point['x'];
    y = point['y'];
  }
}

class Point3D extends Point2D {
  num z;

  Point3D.fromJson(Map<String, num> point)
    : super.fromJson({ 'x': point['x'], 'y': point['y'] }) {
     z = point['z'];
  }
}

```

`Point3D.fromJson` tem um `: super.fromJson(...)` e portanto a ordem de chamada será:

1. Lista de inicialização
2. Point2D.fromJson(...)
3. Point3D.fromJson(...)

De forma semelhante, uma lista de inicialização é definida com uma notação parecida e tem a vantagem de poder definir atributos definidos
com `final`.

```dart

class Point2D {
  final num x;
  final num y;
   
  Point2D.fromJson(Map<String, num> point) 
    : x = point['x'],
      y = point['y'];
}
```

É possível definir construtores constantes em casos que o objeto instânciado nunca serão alterados:

```dart

class ImutablePoint2D {
  final num x;
  final num y;

  const ImutablePoint2D(this.x, this.y);  
}
```

**Observação**: Uma classe que tem um construtor constante não pode ter atributos que não sejam `final`. *De acordo com a documentação,
nem sempre construtores constantes criam constantes, porém não entendi.*

Um método pode definir apenas sua interface, mas deixar sua implementação para outras classes. Chamamos esse tipo de método abstrato e eles
só podem ser existir em uma classe abstrata.

```dart

// abstract class
abstract class Vehicle {
  void move(); // abstract method
}

classes abstratas em dart não podem ser instanciadas e definem interfaces podem em alguns casos ter uma implementação. Veja que foi falado em definir
interfaces. Esse caso é muito comum quando se quer que uma classe tenha a estrutura de uma API de outra classe, porém deseja se fazer uma nova
implementação. Em dart, qualquer classe pode fornecer sua estrutura sem sua implementação No exemplo abaixo, a classe `Car` implementa `Vehicle`

```dart

class Vehicle {
  final String color;
  final String brand;
  
  Vehicle(String color, String brand): this.color = color, this.brand = brand;

  void move() {
    print('Vehicle of brand $brand is moving fast');
  }
}

class Car implements Vehicle {
  final String color;
  final String brand;
  
  int wheels = 4;
  
  Car(String color, String brand) : this.color = color, this.brand = brand;
  
  void move() {
    print('Car of brand $brand with $wheels wheels is moving fast');
  }
}
```

Algumas observações:

1. `Car` não tem a mesma implementação de `Vehicle` mas obrigatoriamente deve ter `color`, `brand` e `move`. 
2. Como `Vehicle` é uma classe comum, não pode ter métodos abstratos e portanto deve implementar seus métodos.
3. O construtor não é herdado em `Car`.
4. Se quisermos apenas uma interface, sem nenhuma implementação, `Vehicle` deve ser uma classe abstrata.

```dart

abstract class Vehicle {
  String color;
  String brand;

  void move();
}

class Car implements Vehicle {
  String color;
  String brand;
  
  int wheels = 4;
  
  Car(this.color, this.brand);
  
  void move() {
    print('Car of brand $brand with $wheels wheels is moving fast');
  }
}
```

**Observação**: Uma classe pode implementar múltiplas outras classes. Para herdar uma implementação, utiliza-se a 
palavra-chave `extends`. Uma subclasse pode sobrescrever um método adicionando uma anotação `@override`.

```dart

@override
void move() { ... }
```

Dart possui herança baseada em mixins(mesclagem?). Uma classe pode fazer mixin utilizando a palavra-chave `with`. Por exemplo:

```dart

mixin FrontEndDeveloper {

  void codeFrontEnd() {
    print('Coding front-end');
  }
}

mixin BackEndDeveloper {
  void codeBackEnd() {
    print('Coding rest API');
  }
}

class Programmer {
  void programmingDumbCode() {
    print('Coding bad stuffs');
  }
}

class Person extends Programmer with FrontEndDeveloper, BackEndDeveloper {
  String name;
  int age;
  
  Person(this.name, this.age);
}
```

Caso não seja necessário utilizar um mixin como uma classe normal, utiliza-se `mixin X { ... }`. É possível restringir um mixin a um
certo tipo com a palavra-chave `on`(`mixin X on Y { ... }`). Com isso, apenas coisas do tipo Y podem usar o mixin X.