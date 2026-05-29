# Introdução e Instalação

Bem-vindo ao primeiro módulo da documentação sobre a linguagem Go.

## O que é Go?

Go (ou Golang) é uma linguagem de programação compilada, de tipagem estática, criada pelo Google em 2009. Ela foi projetada para ser simples, eficiente e segura, com suporte nativo à concorrência.

Seus criadores principais foram:

- Robert Griesemer
- Rob Pike
- Ken Thompson

---

## Por que usar Go?

Go se destaca por:

- **Simplicidade**: sintaxe enxuta e fácil de aprender
- **Performance**: código compilado com desempenho próximo ao C
- **Concorrência nativa**: goroutines e channels integrados à linguagem
- **Tooling robusto**: formatador, testador e gerenciador de módulos já incluídos
- **Comunidade ativa**: amplamente adotado em projetos de infraestrutura e nuvem

---

## Instalação

### Windows

1. Acesse [https://go.dev/dl/](https://go.dev/dl/)
2. Baixe o instalador `.msi` para Windows
3. Execute o instalador e siga as instruções
4. Abra o terminal e verifique a instalação:

```bash
go version
```

### Linux

```bash
# Baixe o pacote (verifique a versão mais recente em go.dev/dl)
wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz

# Extraia para /usr/local
sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz

# Adicione ao PATH no ~/.bashrc ou ~/.zshrc
export PATH=$PATH:/usr/local/go/bin

# Recarregue o shell
source ~/.bashrc

# Verifique
go version
```

### macOS

```bash
# Via Homebrew
brew install go

# Verifique
go version
```

---

## Configurando o ambiente

Após instalar, configure o diretório de trabalho:

```bash
# Crie uma pasta para seus projetos Go
mkdir ~/projetos-go
cd ~/projetos-go

# Inicialize um módulo
go mod init meu-projeto
```

---

## Primeiro programa em Go

Crie um arquivo chamado `main.go`:

```go
package main

import "fmt"

func main() {
    fmt.Println("Olá, Go!")
}
```

Execute com:

```bash
go run main.go
```

Saída esperada:

```
Olá, Go!
```

---

## Estrutura básica de um programa Go

Todo programa Go segue esta estrutura:

- `package main` — define que é o pacote principal (executável)
- `import` — importa pacotes necessários
- `func main()` — ponto de entrada do programa

---
