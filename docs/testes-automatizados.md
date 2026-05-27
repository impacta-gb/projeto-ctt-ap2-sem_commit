# Testes Automatizados na Linguagem Go

Os testes automatizados são fundamentais no desenvolvimento de software moderno, pois garantem que o sistema funcione corretamente mesmo após alterações no código. Na linguagem Go (Golang), o suporte a testes já vem integrado na própria linguagem, tornando o processo simples, eficiente e padronizado.

O Go possui um framework de testes nativo baseado no pacote `testing`, permitindo criar testes unitários, testes de desempenho e validações automatizadas sem necessidade de bibliotecas externas.

---

# Importância dos Testes Automatizados

Os testes automatizados ajudam a:

* identificar erros rapidamente;
* evitar regressões no sistema;
* melhorar a qualidade do código;
* facilitar manutenção;
* aumentar confiabilidade da aplicação.

Em projetos profissionais, testes são considerados parte essencial do desenvolvimento.

---

# Pacote `testing`

O Go utiliza o pacote padrão:

```go id="k9m4pw"
import "testing"
```

Esse pacote fornece recursos para:

* criação de testes;
* validação de resultados;
* execução automatizada;
* medição de desempenho.

---

# Estrutura de Arquivos de Teste

Os arquivos de teste devem terminar com:

```bash id="x7n1ze"
_test.go
```

Exemplo:

```bash id="c4v8jt"
calculadora_test.go
```

---

# Estrutura Básica de um Teste

As funções de teste devem:

* começar com `Test`;
* receber `*testing.T`.

Exemplo:

```go id="y3p7nl"
func TestSomar(t *testing.T) {

}
```

---

# Exemplo de Teste Unitário

Função principal:

```go id="g8v2rm"
func Somar(a int, b int) int {
    return a + b
}
```

Teste:

```go id="d6m1xk"
package main

import "testing"

func TestSomar(t *testing.T) {
    resultado := Somar(2, 3)

    esperado := 5

    if resultado != esperado {
        t.Errorf("Resultado incorreto. Esperado %d, obtido %d", esperado, resultado)
    }
}
```

Nesse exemplo:

* o teste verifica se a função retorna o valor correto;
* `t.Errorf()` informa falha no teste.

---

# Executando Testes

Os testes são executados com o comando:

```bash id="z5k0qy"
go test
```

O Go identifica automaticamente todos os arquivos `_test.go`.

---

# Executando Testes com Detalhes

```bash id="t4p8mw"
go test -v
```

O parâmetro `-v` mostra informações detalhadas da execução.

---

# Testando Múltiplos Cenários

É comum testar diferentes entradas.

```go id="m1z6vh"
func TestSubtrair(t *testing.T) {
    resultado := Subtrair(10, 5)

    if resultado != 5 {
        t.Errorf("Erro esperado: 5")
    }
}
```

---

# Table-Driven Tests

Uma prática muito utilizada em Go é o modelo de testes orientados por tabelas.

Exemplo:

```go id="r9v3tk"
func TestMultiplicar(t *testing.T) {
    testes := []struct {
        a        int
        b        int
        esperado int
    }{
        {2, 3, 6},
        {4, 5, 20},
        {10, 2, 20},
    }

    for _, teste := range testes {
        resultado := Multiplicar(teste.a, teste.b)

        if resultado != teste.esperado {
            t.Errorf(
                "Esperado %d, obtido %d",
                teste.esperado,
                resultado,
            )
        }
    }
}
```

Essa abordagem:

* reduz repetição;
* melhora organização;
* facilita manutenção.

---

# Testando Erros

Também é importante validar situações de erro.

Exemplo:

```go id="n5q8ld"
func TestDividir(t *testing.T) {
    _, err := Dividir(10, 0)

    if err == nil {
        t.Errorf("Era esperado um erro")
    }
}
```

---

# Benchmarks em Go

O Go possui suporte nativo para testes de desempenho.

As funções devem começar com `Benchmark`.

Exemplo:

```go id="w6t1pe"
func BenchmarkSomar(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Somar(2, 3)
    }
}
```

Execução:

```bash id="h2x7mr"
go test -bench=.
```

Os benchmarks ajudam a:

* medir desempenho;
* comparar implementações;
* identificar gargalos.

---

# Cobertura de Testes

O Go consegue medir quanto do código está sendo testado.

Comando:

```bash id="a4m9yt"
go test -cover
```

Exemplo de saída:

```bash id="j7v3fc"
coverage: 85.2% of statements
```

---

# Gerando Relatório de Cobertura

```bash id="u1z8kr"
go test -coverprofile=coverage.out
```

Depois:

```bash id="x3n6wb"
go tool cover -html=coverage.out
```

Isso gera um relatório visual da cobertura.

---

# Testes Paralelos

Go permite execução concorrente de testes.

```go id="e8p2lf"
func TestExemplo(t *testing.T) {
    t.Parallel()

    // teste
}
```

Isso melhora desempenho em projetos grandes.

---

# Organização de Testes

Boas práticas incluem:

* nomes claros;
* testes independentes;
* validações objetivas;
* separação por funcionalidades.

---

# Vantagens dos Testes em Go

O sistema de testes do Go oferece:

* simplicidade;
* integração nativa;
* alta performance;
* fácil automação;
* excelente manutenção.

Além disso, não exige configuração complexa.

---

# Aplicações Práticas

Os testes automatizados são utilizados em:

* APIs REST;
* microsserviços;
* aplicações web;
* sistemas financeiros;
* pipelines CI/CD;
* sistemas distribuídos.

Em ambientes profissionais, testes são essenciais para entrega contínua e qualidade do software.

---

# Considerações Finais

O sistema de testes automatizados da linguagem Go foi desenvolvido para ser simples, rápido e eficiente. Através do pacote `testing`, é possível criar testes unitários, benchmarks e validações automatizadas com pouca complexidade.

O domínio de testes automatizados é indispensável para o desenvolvimento profissional em Go, pois contribui diretamente para estabilidade, confiabilidade e manutenção das aplicações modernas.