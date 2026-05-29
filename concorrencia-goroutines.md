# Concorrência I: Goroutines

Go foi projetado com concorrência como um recurso de primeira classe. As **goroutines** são a unidade básica de concorrência na linguagem — leves, baratas e fáceis de usar.

## O que é uma Goroutine?

Uma goroutine é uma função executada de forma **concorrente** com outras goroutines dentro do mesmo processo. Ela é muito mais leve que uma thread do sistema operacional:

- Uma thread pode ocupar **1 MB** de memória
- Uma goroutine começa com apenas **~2 KB** de stack, crescendo conforme necessário

O runtime do Go gerencia o agendamento das goroutines automaticamente.

---

## Criando uma Goroutine

Basta adicionar `go` antes da chamada de função:

```go
package main

import (
    "fmt"
    "time"
)

func saudacao(nome string) {
    fmt.Printf("Olá, %s!\n", nome)
}

func main() {
    go saudacao("Ana")     // executa concorrentemente
    go saudacao("Rafael")  // executa concorrentemente

    saudacao("main")       // executa normalmente

    time.Sleep(100 * time.Millisecond) // aguarda as goroutines terminarem
}
```

> **Atenção:** sem o `time.Sleep`, o programa pode terminar antes das goroutines concluírem. A solução correta é usar `sync.WaitGroup`.

---

## WaitGroup

`sync.WaitGroup` permite aguardar a conclusão de múltiplas goroutines de forma segura:

```go
package main

import (
    "fmt"
    "sync"
)

func tarefa(id int, wg *sync.WaitGroup) {
    defer wg.Done() // sinaliza que esta goroutine terminou
    fmt.Printf("Tarefa %d concluída\n", id)
}

func main() {
    var wg sync.WaitGroup

    for i := 1; i <= 5; i++ {
        wg.Add(1) // incrementa o contador
        go tarefa(i, &wg)
    }

    wg.Wait() // bloqueia até todas as goroutines terminarem
    fmt.Println("Todas as tarefas concluídas!")
}
```

---

## Mutex — protegendo dados compartilhados

Quando múltiplas goroutines acessam a mesma variável, é necessário sincronizar o acesso para evitar **race conditions**:

```go
package main

import (
    "fmt"
    "sync"
)

type Contador struct {
    mu    sync.Mutex
    valor int
}

func (c *Contador) Incrementar() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.valor++
}

func main() {
    var wg sync.WaitGroup
    contador := Contador{}

    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            contador.Incrementar()
        }()
    }

    wg.Wait()
    fmt.Println("Valor final:", contador.valor) // sempre 1000
}
```

---

## Detectando Race Conditions

Go possui um detector de race conditions integrado. Execute com:

```bash
go run -race main.go
```

---

## Goroutines anônimas

Você pode criar goroutines com funções anônimas:

```go
for i := 0; i < 3; i++ {
    i := i // captura o valor atual (importante!)
    go func() {
        fmt.Println("Goroutine:", i)
    }()
}
```

> **Atenção:** sempre capture variáveis do loop em uma nova variável dentro do loop para evitar o problema clássico de closure em goroutines.

---

## Exemplo completo

```go
package main

import (
    "fmt"
    "sync"
    "time"
)

func processarPedido(id int, wg *sync.WaitGroup) {
    defer wg.Done()
    fmt.Printf("Processando pedido #%d...\n", id)
    time.Sleep(50 * time.Millisecond) // simula trabalho
    fmt.Printf("Pedido #%d concluído!\n", id)
}

func main() {
    var wg sync.WaitGroup
    pedidos := []int{101, 102, 103, 104, 105}

    inicio := time.Now()

    for _, id := range pedidos {
        wg.Add(1)
        go processarPedido(id, &wg)
    }

    wg.Wait()
    fmt.Printf("\nTodos os pedidos processados em %v\n", time.Since(inicio))
}
```

---
