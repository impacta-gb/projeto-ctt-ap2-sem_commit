# Arrays, Slices e Maps
 
Neste módulo você aprenderá as principais estruturas de dados nativas da linguagem Go: arrays de tamanho fixo, slices dinâmicos e maps (dicionários).
 
## Arrays
 
Arrays em Go têm **tamanho fixo** definido em tempo de compilação:
 
```go
var numeros [5]int
numeros[0] = 10
numeros[1] = 20
 
// Declaração com inicialização
frutas := [3]string{"maçã", "banana", "laranja"}
 
// O compilador conta os elementos automaticamente
cores := [...]string{"azul", "verde", "vermelho"}
```
 
Acessando elementos:
 
```go
fmt.Println(frutas[0]) // maçã
fmt.Println(len(frutas)) // 3
```
 
---
 
## Slices
 
Slices são mais usados que arrays em Go. Eles têm **tamanho dinâmico** e são mais flexíveis:
 
```go
// Criando um slice
numeros := []int{1, 2, 3, 4, 5}
 
// Criando com make
nomes := make([]string, 3)       // tamanho 3
buffer := make([]int, 3, 10)     // tamanho 3, capacidade 10
```
 
### Adicionando elementos com `append`
 
```go
lista := []string{"Go", "Python"}
lista = append(lista, "Rust")
lista = append(lista, "Java", "C++")
 
fmt.Println(lista) // [Go Python Rust Java C++]
```
 
### Fatiamento (slicing)
 
```go
numeros := []int{10, 20, 30, 40, 50}
 
fmt.Println(numeros[1:3])  // [20 30]
fmt.Println(numeros[:2])   // [10 20]
fmt.Println(numeros[3:])   // [40 50]
```
 
### Iterando com range
 
```go
linguagens := []string{"Go", "Python", "Rust"}
 
for i, lang := range linguagens {
    fmt.Printf("%d: %s\n", i, lang)
}
```
 
### Len e Cap
 
```go
s := make([]int, 3, 5)
fmt.Println(len(s)) // 3 — elementos atuais
fmt.Println(cap(s)) // 5 — capacidade total
```
 
---
 
## Maps
 
Maps armazenam pares **chave → valor**:
 
```go
// Declaração
idades := map[string]int{
    "Ana":    22,
    "Rafael": 25,
    "Beatriz": 21,
}
 
// Criando com make
capitais := make(map[string]string)
capitais["Brasil"] = "Brasília"
capitais["França"] = "Paris"
```
 
### Lendo valores
 
```go
fmt.Println(idades["Ana"]) // 22
```
 
### Verificando se a chave existe
 
```go
valor, existe := idades["Ruth"]
if existe {
    fmt.Println("Idade:", valor)
} else {
    fmt.Println("Chave não encontrada")
}
```
 
### Deletando uma chave
 
```go
delete(idades, "Ana")
```
 
### Iterando sobre um map
 
```go
for nome, idade := range idades {
    fmt.Printf("%s tem %d anos\n", nome, idade)
}
```
 
---
 
## Comparativo
 
| | Array | Slice | Map |
|---|---|---|---|
| Tamanho | Fixo | Dinâmico | Dinâmico |
| Chave | Índice inteiro | Índice inteiro | Qualquer tipo comparável |
| Uso típico | Dados fixos | Listas | Dicionários |
 
---
 
## Exemplo completo
 
```go
package main
 
import "fmt"
 
func main() {
    notas := map[string][]float64{
        "Ana":    {8.5, 9.0, 7.5},
        "Rafael": {6.0, 7.0, 8.0},
    }
 
    for aluno, valores := range notas {
        soma := 0.0
        for _, v := range valores {
            soma += v
        }
        media := soma / float64(len(valores))
        fmt.Printf("%s — média: %.2f\n", aluno, media)
    }
}
```
 
---
