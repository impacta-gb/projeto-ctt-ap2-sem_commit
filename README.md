# Documentação da Linguagem Go

Documentação técnica da linguagem Go desenvolvida com Zensical, publicada automaticamente via GitHub Pages através de um pipeline de CI/CD com GitHub Actions.

---

# Integrantes

| Nome                         | GitHub           | RA      |
| ---------------------------- | ---------------- | ------- |
| Ana Luiza Corrêa de Oliveira | @analu007        | 2500933 |
| Beatriz Lino dos Passos      | @BiiaLino        | 2501401 |
| Rafael Antonio Tomé Ferreira | @rafaeltome-tech | 2501412 |
| Ruth da Silva Gama           | @gamaruthdev     | 2403586 |

---

# Sobre o Projeto

Este projeto tem como objetivo apresentar os principais conceitos da linguagem Go de forma organizada e acessível, abordando os seguintes tópicos:

* Introdução e Instalação
* Sintaxe Básica e Variáveis
* Estruturas de Controle (`if`, `for`, `switch`)
* Arrays, Slices e Maps
* Structs e Métodos
* Tratamento de Erros (*Error Handling*)
* Concorrência I: Goroutines
* Concorrência II: Channels
* Gerenciamento de Pacotes (*Go Modules*)
* Testes Automatizados em Go

---

# Tecnologias Utilizadas

* Go
* Markdown
* Zensical
* GitHub Actions
* GitHub Pages

---

# Fluxo de Trabalho Colaborativo

A equipe adotou o modelo de **Feature Branches com Pull Requests**, seguindo as boas práticas de desenvolvimento colaborativo.

---

# Proteção da Branch Main

A branch `main` foi configurada com regras de proteção (*Branch Protection Rules*) pela Ana Luiza, garantindo que:

* Commits diretos na `main` são bloqueados
* Toda alteração deve ser feita via Pull Request
* É obrigatória a aprovação de pelo menos um outro membro antes do merge

---

# Criação de Branches

Para cada nova página de documentação, o integrante responsável criou uma branch separada seguindo o padrão:

```bash
feat/<nome-do-topico>
```

## Exemplos

```bash
feat/introducao-instalacao
feat/arrays-slices-maps
feat/concorrencia-goroutines
```

---

# Abertura de Pull Requests

Ao finalizar o conteúdo, o integrante abriu um Pull Request para a `main` com um título descritivo seguindo o padrão:

```bash
docs: <nome do tópico>
```

---

# Code Review

As revisões foram feitas por todos os integrantes da equipe — quem estivesse disponível primeiro realizava a revisão, deixava comentários quando necessário e aprovava o PR.

Após a aprovação, o merge era realizado na `main`.

---

# Arquitetura do Workflow (GitHub Actions)

O workflow foi desenvolvido pelo Rafael, localizado em:

```bash
.github/workflows/
```

---

# Gatilhos (Triggers)

O pipeline é executado nos seguintes eventos:

* `pull_request` para a branch `main` — valida o build antes do merge
* `push` para a branch `main` — executa após o merge do PR
* `schedule` com cron `0 0 * * 0` — executa automaticamente toda semana

---

# Jobs

O workflow é dividido em dois jobs com responsabilidades separadas.

## `build_site`

* Utiliza Matrix Strategy com Python 3.10 e 3.11 para garantir compatibilidade
* Implementa cache das dependências Python via `actions/cache`
* Instala o Zensical e executa o build da documentação
* Faz upload dos arquivos HTML gerados como artefato

## `deploy_site`

* Aguarda a conclusão do `build_site` via diretiva `needs:`
* Faz download do artefato gerado pelo job anterior
* Publica a documentação no GitHub Pages
* Só é executado em `push` na `main` ou no evento `schedule`
* Nunca é executado durante Pull Requests, garantido pela diretiva `if:`

---

# Fluxo do Pipeline

```text
Pull Request aberto
 ↓
build_site roda (matrix: Python 3.10 e 3.11)
 ↓
Build OK? → Reviewer aprova → Merge na main
 ↓
build_site roda novamente
 ↓
deploy_site baixa o artefato e publica no GitHub Pages
```

---

# Site Publicado

Acesse a documentação em:

```text
https://impacta-gb.github.io/projeto-ctt-ap2-sem_commit/
```

---
[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/3P1cAu_6)
