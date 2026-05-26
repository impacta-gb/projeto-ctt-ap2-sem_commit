Sintaxe Básica e Variáveis
Neste módulo você aprenderá como Go organiza seu código, como declarar variáveis e quais são os tipos de dados disponíveis na linguagem.
Pacotes
Todo arquivo Go pertence a um pacote. O pacote main é o ponto de entrada de programas executáveis:
package main
Pacotes de biblioteca usam outros nomes:
package utils

Importações
Use import para incluir pacotes:
import "fmt"

// Múltiplos pacotes
import (
    "fmt"
    "math"
    "strings"
)

Variáveis
Declaração com var
var nome string = "Go"
var versao int = 1
var ativo bool = true
Declaração curta com :=
Dentro de funções, você pode usar a forma curta:
nome := "Go"
versao := 1
ativo := true
Múltiplas variáveis
var (
    linguagem string = "Go"
    ano       int    = 2009
    opensource bool  = true
)

Tipos de dados
Tipo	Descrição	Exemplo
int	Inteiro	42
float64	Ponto flutuante	3.14
string	Texto	"Olá"
bool	Booleano	true / false
byte	Alias para uint8	'A'
rune	Alias para int32 (caractere Unicode)	'á'


Constantes
Constantes são declaradas com const e não podem ser alteradas:
const Pi = 3.14159
const Linguagem = "Go"

Valor zero
Em Go, toda variável declarada sem valor inicial recebe o valor zero do seu tipo:
var numero int    // 0
var texto string  // ""
var ativo bool    // false

Conversão de tipos
Go não faz conversão implícita. É necessário converter explicitamente:
var x int = 10
var y float64 = float64(x)
var z int = int(y)

Funções básicas do pacote fmt
fmt.Println("Texto com quebra de linha")
fmt.Print("Texto sem quebra de linha")
fmt.Printf("Nome: %s, Idade: %d\n", "Go", 15)
Principais verbos de formatação:
    • %s — string
    • %d — inteiro
    • %f — float
    • %v — valor genérico
    • %T — tipo da variável

Exemplo completo
package main

import "fmt"

func main() {
    linguagem := "Go"
    ano := 2009
    var estavel bool = true

    fmt.Printf("Linguagem: %s\n", linguagem)
    fmt.Printf("Criada em: %d\n", ano)
    fmt.Printf("Estável: %v\n", estavel)
}

Próximos passos
Continue para Estruturas de Controle, onde você aprenderá if, for e switch em Go.
