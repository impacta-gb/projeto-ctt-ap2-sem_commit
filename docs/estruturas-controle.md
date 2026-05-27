# Estruturas de Controle (If, For, Switch)
 
Go possui um conjunto enxuto de estruturas de controle. Não há `while` nem `do-while` — o `for` cobre todos esses casos.
 
## If / Else
 
A sintaxe do `if` em Go não usa parênteses na condição:
 
```go
idade := 18
 
if idade >= 18 {
    fmt.Println("Maior de idade")
} else {
    fmt.Println("Menor de idade")
}
```
 
### If com inicialização
 
Go permite declarar uma variável diretamente no `if`:
 
```go
if nota := 7.5; nota >= 6.0 {
    fmt.Println("Aprovado")
} else {
    fmt.Println("Reprovado")
}
// "nota" existe apenas dentro do bloco if/else
```
 
### If / Else If / Else
 
```go
pontuacao := 85
 
if pontuacao >= 90 {
    fmt.Println("A")
} else if pontuacao >= 70 {
    fmt.Println("B")
} else if pontuacao >= 50 {
    fmt.Println("C")
} else {
    fmt.Println("F")
}
```
 
---
 
## For
 
O `for` é a única estrutura de repetição em Go e pode ser usada de três formas.
 
### Forma clássica (equivale ao for do C)
 
```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```
 
### Forma condicional (equivale ao while)
 
```go
contador := 0
 
for contador < 5 {
    fmt.Println(contador)
    contador++
}
```
 
### Loop infinito
 
```go
for {
    fmt.Println("Executando...")
    break // necessário para sair
}
```
 
### For com range
 
Usado para iterar sobre slices, arrays, maps e strings:
 
```go
linguagens := []string{"Go", "Python", "Rust"}
 
for i, lang := range linguagens {
    fmt.Printf("%d: %s\n", i, lang)
}
 
// Ignorando o índice com _
for _, lang := range linguagens {
    fmt.Println(lang)
}
```
 
### Break e Continue
 
```go
for i := 0; i < 10; i++ {
    if i == 3 {
        continue // pula o 3
    }
    if i == 7 {
        break // para no 7
    }
    fmt.Println(i)
}
```
 
---
 
## Switch
 
O `switch` em Go não precisa de `break` — cada `case` é automaticamente encerrado:
 
```go
dia := "segunda"
 
switch dia {
case "segunda", "terça", "quarta", "quinta", "sexta":
    fmt.Println("Dia útil")
case "sábado", "domingo":
    fmt.Println("Final de semana")
default:
    fmt.Println("Dia inválido")
}
```
 
### Switch com expressão
 
```go
nota := 8
 
switch {
case nota >= 9:
    fmt.Println("Excelente")
case nota >= 7:
    fmt.Println("Bom")
case nota >= 5:
    fmt.Println("Regular")
default:
    fmt.Println("Insuficiente")
}
```
 
### Fallthrough
 
Use `fallthrough` para executar o próximo `case` intencionalmente:
 
```go
x := 1
 
switch x {
case 1:
    fmt.Println("Um")
    fallthrough
case 2:
    fmt.Println("Dois")
case 3:
    fmt.Println("Três")
}
// Saída: Um, Dois
```
 
---
 
## Exemplo completo
 
```go
package main
 
import "fmt"
 
func main() {
    numeros := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
 
    for _, n := range numeros {
        if n%2 == 0 {
            fmt.Printf("%d é par\n", n)
        } else {
            fmt.Printf("%d é ímpar\n", n)
        }
    }
}
```
 
---