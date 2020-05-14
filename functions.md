# Funções

Como foi mencionado nas sessões anteriores, praticamente tudo é um objeto em Dart. Uma função também é um objeto. Ela pode ser declarada de
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

Todos os exemplos dados, é informado o tipo de retorno da função. Essa informação pode ser omitida já que Dart infere tipos. Logo:

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