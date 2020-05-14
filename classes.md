# Classes

Todo objeto em Dart é moldado por uma classe. Diferente de Java, Dart possui uma herança baseada  em mixin.
Todas as classes, com exceção de Object, possuem uma super classe, porém o corpo de uma classe pode ser reutilizado 
através de mesclagem de classes.

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

Um construtor é uma função responsável por inicializar um objeto. Em Dart existem construtores da forma `ClassName` e 
`ClassName.namedConstructor`.

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

É possível definir construtores constantes em casos que o objeto instânciado nunca devem ser alterados:

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
só podem existir em uma classe abstrata.

```dart

// abstract class
abstract class Vehicle {
  void move(); // abstract method
}

classes abstratas em dart não podem ser instanciadas e definem interfaces. Seus métodos podem em alguns casos ter uma implementação.
Veja que foi falado em definir interfaces. Esse caso é muito comum quando se quer que uma classe tenha a estrutura de uma de outra classe, 
porém deseja se fazer uma nova implementação. Em dart, qualquer classe pode fornecer sua estrutura. No exemplo abaixo, 
a classe `Car` implementa `Vehicle`

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

Uma instância de uma classe pode ser chamada como uma função se possuir o método `call`. Veja o exemplo abaixo:

```dart

class Sum {
  num call(num a, num b) => a + b;
}

main() {
  var sum = Sum();
 
  print(sum(2, 2));
}
```