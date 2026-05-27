# Concorrência em Go: Channels

Os `channels` são um dos principais mecanismos de comunicação entre goroutines na linguagem Go (Golang). Eles foram criados para permitir troca segura de dados entre tarefas concorrentes, evitando problemas comuns de sincronização, como race conditions e inconsistência de memória.

Na filosofia do Go, existe um princípio bastante conhecido:

> “Não compartilhe memória para se comunicar; comunique-se para compartilhar memória.”

Os channels seguem exatamente essa ideia, permitindo que goroutines troquem informações de forma organizada e segura.

---

# O que são Channels

Channels são estruturas utilizadas para enviar e receber dados entre goroutines.

Eles funcionam como “canais de comunicação”, permitindo que uma goroutine envie informações enquanto outra recebe esses dados.

---

# Criando um Channel

Os channels são criados utilizando a função `make()`.

## Sintaxe Básica

```go id="s7x2qm"
canal := make(chan int)
```

Nesse exemplo:

* `chan int` indica que o channel transporta valores inteiros;
* `make()` cria o canal na memória.

---

# Enviando Dados para um Channel

O operador `<-` é utilizado para enviar valores.

```go id="y4m8vn"
canal <- 10
```

Nesse caso:

* o valor `10` é enviado para o channel.

---

# Recebendo Dados de um Channel

O mesmo operador também é utilizado para receber valores.

```go id="d9p5zw"
valor := <-canal
```

Aqui:

* a goroutine aguarda um valor chegar no canal;
* o valor recebido é armazenado na variável.

---

# Exemplo Básico

```go id="u6j1ra"
package main

import "fmt"

func main() {
    canal := make(chan int)

    go func() {
        canal <- 100
    }()

    valor := <-canal

    fmt.Println(valor)
}
```

Nesse exemplo:

* uma goroutine envia o valor `100`;
* a função principal recebe e imprime o valor.

---

# Comunicação Síncrona

Por padrão, channels são bloqueantes.

Isso significa:

* o envio espera alguém receber;
* o recebimento espera alguém enviar.

Esse comportamento ajuda na sincronização automática entre goroutines.

---

# Channels Tipados

Cada channel transporta apenas um tipo específico de dado.

Exemplos:

```go id="z8m2qy"
chan int
chan string
chan bool
```

Isso aumenta a segurança do código e evita erros de tipo.

---

# Channels com Buffer

Também existem channels com buffer, capazes de armazenar múltiplos valores temporariamente.

## Criação de Channel com Buffer

```go id="g5w1pf"
canal := make(chan int, 3)
```

Nesse caso:

* o canal suporta até 3 valores sem bloquear imediatamente.

---

# Exemplo de Buffer

```go id="h0q7ze"
canal := make(chan int, 2)

canal <- 10
canal <- 20

fmt.Println(<-canal)
fmt.Println(<-canal)
```

Como o buffer suporta dois elementos:

* os envios não bloqueiam imediatamente.

---

# Fechando um Channel

A função `close()` encerra um channel.

```go id="j3v9nb"
close(canal)
```

Após fechado:

* não é possível enviar novos valores;
* os valores restantes ainda podem ser recebidos.

---

# Verificando se o Channel Foi Fechado

```go id="k7n2yt"
valor, aberto := <-canal
```

Nesse caso:

* `aberto` será `false` se o canal estiver fechado.

---

# Percorrendo Channels com `range`

Channels podem ser percorridos com `range`.

```go id="m8x6lc"
for valor := range canal {
    fmt.Println(valor)
}
```

O laço termina automaticamente quando o canal é fechado.

---

# Channels Unidirecionais

Go permite restringir channels apenas para envio ou recebimento.

## Apenas envio

```go id="p4j8dw"
func enviar(canal chan<- int)
```

## Apenas recebimento

```go id="t1q5vk"
func receber(canal <-chan int)
```

Isso melhora:

* legibilidade;
* segurança;
* organização do código.

---

# Exemplo com Goroutines

```go id="r9m2xo"
package main

import (
    "fmt"
    "time"
)

func processar(canal chan string) {
    time.Sleep(time.Second)

    canal <- "Processamento concluído"
}

func main() {
    canal := make(chan string)

    go processar(canal)

    mensagem := <-canal

    fmt.Println(mensagem)
}
```

Nesse exemplo:

* uma goroutine executa processamento;
* o resultado é enviado para o channel;
* a função principal aguarda a resposta.

---

# Select em Channels

O comando `select` permite aguardar múltiplos channels simultaneamente.

```go id="x5z0nr"
select {
case msg := <-canal1:
    fmt.Println(msg)

case msg := <-canal2:
    fmt.Println(msg)
}
```

O `select` executa o primeiro channel disponível.

---

# Deadlocks

Um deadlock ocorre quando goroutines ficam esperando indefinidamente umas pelas outras.

Exemplo comum:

```go id="w3k7pa"
canal := make(chan int)

canal <- 10
```

Nesse caso:

* ninguém está recebendo o valor;
* o programa trava.

O Go detecta deadlocks automaticamente em tempo de execução.

---

# Vantagens dos Channels

Os channels oferecem diversos benefícios:

* comunicação segura entre goroutines;
* sincronização automática;
* redução de race conditions;
* código concorrente mais organizado;
* melhor escalabilidade.

---

# Aplicações Práticas

Channels são muito utilizados em:

* sistemas distribuídos;
* filas de processamento;
* workers concorrentes;
* pipelines de dados;
* APIs assíncronas;
* sistemas em tempo real.

---

# Considerações Finais

Os channels são um dos pilares do modelo de concorrência da linguagem Go. Eles permitem comunicação eficiente e segura entre goroutines, reduzindo a complexidade associada à sincronização manual de threads.

Combinados com goroutines, os channels tornam o Go extremamente poderoso para desenvolvimento de aplicações concorrentes, escaláveis e de alta performance, sendo amplamente utilizados em ambientes cloud-native, microsserviços e sistemas distribuídos modernos.