# Structs e Métodos
 
Go não é uma linguagem orientada a objetos no sentido tradicional, mas utiliza **structs** e **métodos** para organizar dados e comportamentos de forma semelhante.
 
## Structs
 
Uma struct é um tipo composto que agrupa campos relacionados:
 
```go
type Pessoa struct {
    Nome  string
    Idade int
    Email string
}
```
 
### Criando instâncias
 
```go
// Inicialização com nomes dos campos
p1 := Pessoa{
    Nome:  "Ana",
    Idade: 22,
    Email: "ana@email.com",
}
 
// Inicialização por posição (menos recomendada)
p2 := Pessoa{"Rafael", 25, "rafael@email.com"}
 
// Declaração e atribuição separadas
var p3 Pessoa
p3.Nome = "Beatriz"
p3.Idade = 21
```
 
### Acessando campos
 
```go
fmt.Println(p1.Nome)  // Ana
fmt.Println(p1.Idade) // 22
```
 
---
 
## Métodos
 
Métodos são funções associadas a um tipo. Em Go, você define um método com um **receiver**:
 
```go
type Retangulo struct {
    Largura float64
    Altura  float64
}
 
// Método com value receiver
func (r Retangulo) Area() float64 {
    return r.Largura * r.Altura
}
 
func (r Retangulo) Perimetro() float64 {
    return 2 * (r.Largura + r.Altura)
}
```
 
Usando o método:
 
```go
rect := Retangulo{Largura: 5.0, Altura: 3.0}
fmt.Println(rect.Area())      // 15
fmt.Println(rect.Perimetro()) // 16
```
 
---
 
## Pointer Receiver
 
Use pointer receiver quando precisar **modificar** os campos da struct:
 
```go
type Contador struct {
    Valor int
}
 
// Value receiver — NÃO modifica o original
func (c Contador) IncrementarValor() {
    c.Valor++ // afeta apenas a cópia local
}
 
// Pointer receiver — modifica o original
func (c *Contador) Incrementar() {
    c.Valor++
}
```
 
```go
c := Contador{Valor: 0}
c.Incrementar()
c.Incrementar()
fmt.Println(c.Valor) // 2
```
 
---
 
## Structs aninhadas
 
```go
type Endereco struct {
    Rua    string
    Cidade string
    Estado string
}
 
type Funcionario struct {
    Nome     string
    Salario  float64
    Endereco Endereco
}
 
f := Funcionario{
    Nome:    "Ruth",
    Salario: 4500.00,
    Endereco: Endereco{
        Rua:    "Av. Paulista",
        Cidade: "São Paulo",
        Estado: "SP",
    },
}
 
fmt.Println(f.Endereco.Cidade) // São Paulo
```
 
---
 
## Interfaces
 
Go usa interfaces para definir comportamentos. Qualquer tipo que implemente os métodos de uma interface a satisfaz automaticamente:
 
```go
type Forma interface {
    Area() float64
    Perimetro() float64
}
 
type Circulo struct {
    Raio float64
}
 
func (c Circulo) Area() float64 {
    return 3.14159 * c.Raio * c.Raio
}
 
func (c Circulo) Perimetro() float64 {
    return 2 * 3.14159 * c.Raio
}
 
func imprimirInfo(f Forma) {
    fmt.Printf("Área: %.2f | Perímetro: %.2f\n", f.Area(), f.Perimetro())
}
```
 
```go
r := Retangulo{Largura: 4, Altura: 3}
c := Circulo{Raio: 5}
 
imprimirInfo(r)
imprimirInfo(c)
```
 
---
 
## Exemplo completo
 
```go
package main
 
import "fmt"
 
type Produto struct {
    Nome     string
    Preco    float64
    Estoque  int
}
 
func (p *Produto) Desconto(percentual float64) {
    p.Preco -= p.Preco * (percentual / 100)
}
 
func (p Produto) Disponivel() bool {
    return p.Estoque > 0
}
 
func main() {
    produto := Produto{Nome: "Teclado", Preco: 200.00, Estoque: 5}
    produto.Desconto(10)
    fmt.Printf("Produto: %s | Preço: R$%.2f | Disponível: %v\n",
        produto.Nome, produto.Preco, produto.Disponivel())
}
```
 
---
