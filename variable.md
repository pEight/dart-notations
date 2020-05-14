# Variaveis

Uma váriavel é um recurso que armazena uma referência para um objeto em memória. Declaramos uma váriavel da seguinte forma:

```dart

var foo = 'Some String'
```

A linguagem infere o tipo da variável e portanto não é preciso informá-lo. Se for optado
por explicitar o tipo, é preciso substituir `var` pelo tipo em questão.

```dart

String foo = 'Some String';
```

Não passando nenhum valor para uma váriavel faz com que seu valor inicial seja `null`. Para tornar uma variável imutavel,
troca-se `var` por `final` ou `const`. Uma variável `final` pode receber o valor uma única vez em seu tempo de vida.
Uma `const` variável é constante em tempo de compilação.

```dart

final foo = 'Some Final String';

final Int baz = 7;
```

# Coleções

Aqui segue alguns objetos com tratamento especial em Dart.

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