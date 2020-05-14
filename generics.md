# Tipos genérico

```dart

List<int> l;
```

Após o tipo `List`, existe a seguinte notação: `<int>`. Esse trecho informa que l será uma lista de inteiros e portanto se for inserido um
valor diferente do tipo inteiro, ocorrerá um erro de compilação. Generics ajudam nosso código a ter uma tipagem mais segura, melhor 
documentada e que evita duplicação de código. Para a última vantagem citada, generics permite que seja compartilhada uma única interface 
entre tipos diferentes.

Uma diferença em Tipos genéricos de Java para Dart é que na linguagem criada pela google elas podem ser testadas em tempo de execução.

```dart

var l = List<String>();

l.addAll(['a', 'b', 'c']);

print(l is List<String>); // true
```

Uma função pode também utilizar tipos genéricos.

```dart

T someFunc<T>(T foo) {
  return foo;
}

main() {
  var bar = someFunc<String>('some text');
  
  print(bar);
}
```
