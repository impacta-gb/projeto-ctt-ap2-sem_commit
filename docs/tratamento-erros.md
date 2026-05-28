# Tratamento de Erros (Error Handling)
 
Em Go, erros são valores. Não existe exceção (`try/catch`) como em outras linguagens — o tratamento de erros é explícito e feito via retorno de valores.
 
## O tipo `error`
 
`error` é uma interface nativa de Go:
 
```go
type error interface {
    Error() string
}
```
 
Funções que podem falhar retornam `error` como último valor:
 
```go
import (
    "fmt"
    "strconv"
)
 
func main() {
    numero, err := strconv.Atoi("123")
    if err != nil {
        fmt.Println("Erro:", err)
        return
    }
    fmt.Println("Número:", numero)
}
```
 
---
 
## Padrão de verificação de erro
 
O padrão idiomático em Go é sempre verificar o erro logo após a chamada:
 
```go
resultado, err := algumFuncao()
if err != nil {
    // trata o erro
    return
}
// usa o resultado com segurança
```
 
---
 
## Criando erros
 
### Com `errors.New`
 
```go
import "errors"
 
func dividir(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("divisão por zero não é permitida")
    }
    return a / b, nil
}
```
 
### Com `fmt.Errorf`
 
Permite formatar a mensagem de erro com contexto:
 
```go
import "fmt"
 
func buscarUsuario(id int) (string, error) {
    if id <= 0 {
        return "", fmt.Errorf("id inválido: %d", id)
    }
    return "Ana", nil
}
```
 
---
 
## Erros customizados
 
Você pode criar tipos de erro personalizados implementando a interface `error`:
 
```go
type ErroValidacao struct {
    Campo   string
    Mensagem string
}
 
func (e *ErroValidacao) Error() string {
    return fmt.Sprintf("campo '%s': %s", e.Campo, e.Mensagem)
}
 
func validarIdade(idade int) error {
    if idade < 0 {
        return &ErroValidacao{
            Campo:    "idade",
            Mensagem: "não pode ser negativa",
        }
    }
    return nil
}
```
 
Verificando o tipo do erro com `errors.As`:
 
```go
err := validarIdade(-1)
var erroVal *ErroValidacao
if errors.As(err, &erroVal) {
    fmt.Println("Erro de validação no campo:", erroVal.Campo)
}
```
 
---
 
## Wrapping de erros
 
Go permite encapsular erros para adicionar contexto, mantendo o erro original:
 
```go
err := fmt.Errorf("falha ao processar pedido: %w", errOriginal)
 
// Desempacotando com errors.Unwrap
erroInterno := errors.Unwrap(err)
 
// Verificando o tipo interno com errors.Is
if errors.Is(err, os.ErrNotExist) {
    fmt.Println("Arquivo não encontrado")
}
```
 
---
 
## Panic e Recover
 
`panic` interrompe o fluxo normal do programa. Use apenas em situações realmente inesperadas:
 
```go
func dividir(a, b int) int {
    if b == 0 {
        panic("divisão por zero")
    }
    return a / b
}
```
 
`recover` captura um panic dentro de um `defer`:
 
```go
func executarSeguro() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recuperado do panic:", r)
        }
    }()
 
    dividir(10, 0)
}
```
 
> **Atenção:** prefira sempre retornar `error` em vez de usar `panic`. Reserve o `panic` para erros de programação irrecuperáveis.
 
---
 
## Exemplo completo
 
```go
package main
 
import (
    "errors"
    "fmt"
)
 
var ErrSaldoInsuficiente = errors.New("saldo insuficiente")
 
type ContaBancaria struct {
    Titular string
    Saldo   float64
}
 
func (c *ContaBancaria) Sacar(valor float64) error {
    if valor <= 0 {
        return fmt.Errorf("valor inválido para saque: %.2f", valor)
    }
    if valor > c.Saldo {
        return fmt.Errorf("tentativa de saque de R$%.2f: %w", valor, ErrSaldoInsuficiente)
    }
    c.Saldo -= valor
    return nil
}
 
func main() {
    conta := ContaBancaria{Titular: "Ana", Saldo: 500.00}
 
    err := conta.Sacar(600.00)
    if err != nil {
        if errors.Is(err, ErrSaldoInsuficiente) {
            fmt.Println("Operação negada:", err)
        } else {
            fmt.Println("Erro:", err)
        }
        return
    }
 
    fmt.Printf("Saque realizado. Saldo restante: R$%.2f\n", conta.Saldo)
}
```
 
---
