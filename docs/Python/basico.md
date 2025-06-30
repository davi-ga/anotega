---
sidebar_position: 2
---

# Python Básico

## O que é Python?

Python é uma linguagem de programação de alto nível, interpretada e de tipagem dinâmica. Permitindo Duck Typing e Gradual Typing. É uma linguagem de fácil leitura e escrita, o que a torna ideal para iniciantes e para desenvolvimento rápido de aplicações.  

O Python suporta diferentes paradigmas de programação, incluindo programação orientada a objetos, programação funcional e programação imperativa. Internamente, tudo no Python é um `objeto`.

:::tip Duck Typing
    Duck Typing é um conceito de programação que se refere à ideia de que o tipo ou classe de um objeto é menos importante do que os métodos que ele implementa. Em outras palavras, se um objeto se comporta como um determinado tipo, ele pode ser tratado como esse tipo, independentemente de sua classe real. Isso permite maior flexibilidade e reutilização de código.
:::

:::tip Gradual Typing
    Gradual Typing é um sistema de tipos que combina tipagem dinâmica e tipagem estática. Isso significa que você pode optar por adicionar anotações de tipo ao seu código, mas não é obrigatório. Isso permite que você escreva código rapidamente, mas também tenha a opção de adicionar segurança de tipo quando necessário.
:::

## Variáveis

Variáveis são usadas para armazenar dados. Você pode criar uma variável atribuindo um valor a ela usando o operador de atribuição `=`. O Python suporta vários tipos de dados, incluindo números inteiros, números de ponto flutuante, strings e listas.

Variáveis são nomeadas em `snake_case` e devem começar com uma letra ou um caractere de sublinhado `_`. O nome da variável pode conter letras, números e caracteres de sublinhado, mas não pode conter espaços ou caracteres especiais.

### Exemplos de variáveis

```python
    # Números inteiros
    idade = 30

    # Números de ponto flutuante
    altura = 1.75

    # Strings
    nome = "João"

    # Listas
    frutas = ["maçã", "banana", "laranja"]

    # Dicionários
    pessoa = {
        "nome": "João",
        "idade": 30,
        "altura": 1.75
    }
    # Tuplas
    coordenadas_tupla = (10, 20)
```

## Constantes
Constantes são variáveis cujo valor não deve ser alterado durante a execução do programa. No Python, não há uma maneira nativa de declarar constantes, mas é uma convenção usar letras maiúsculas em `SCREAMING_SNAKE_CASE`.

### Exemplos de constantes

```python
    # Constantes
    PI = 3.14
    NOME_DO_PROJETO = "Meu Projeto"
```

## Listas

```python	

    def create_fake_card(self):
        card_elements_with_numbers = ['']
        while len(card_elements_with_numbers[0]) < 13 or len(card_elements_with_numbers[0]) > 19:
            card = fake.credit_card_full().replace("\n", " ")
            card_elements = card.split(" ")
            card_elements_with_numbers = [
                element
                for element in card_elements
                if any(char.isdigit() for char in element)
            ]
        return card_elements_with_numbers

```

Esta função cria um número de cartão de crédito falso. O número do cartão é gerado pela biblioteca `Faker` e é validado para ter entre 13 e 19 dígitos, card_elements_with_numbers é uma lista que armazena os elementos do cartão que contém números.

## Funções
Funções são blocos de código reutilizáveis que realizam uma tarefa específica. Você pode definir uma função usando a palavra-chave `def`, seguida pelo nome da função e parênteses. Os parâmetros da função são definidos entre os parênteses.  

As funções podem ter parâmetros obrigatórios e opcionais. Os parâmetros obrigatórios devem ser fornecidos ao chamar a função, enquanto os parâmetros opcionais têm um valor padrão.

As funções podem retornar valores usando a palavra-chave `return`. Se uma função não retornar um valor, ela retornará `None` por padrão.

### Exemplos de funções

```python
    def soma(a: int, b: int) -> int:
       
        return a + b

    def media(numeros: list) -> float:
       
        return sum(numeros) / len(numeros)
```
### Chamando funções

Funções são chamadas pelo nome da função seguido por parênteses. Os argumentos são passados entre os parênteses. Você pode passar argumentos posicionais ou nomeados.

:::tip Notação de ponto(.)  
    A notação . é usado para chamar métodos de objetos. Se você tiver um objeto `pessoa` com um método `falar`, você pode chamá-lo assim: `pessoa.falar()`. 
:::


```python
    # Chamando a função soma com parâmetros posicionais
    resultado = soma(10, 5)
    print(resultado) 

    # Chamando a função media com parâmetros posicionais
    numeros = [1, 2, 3, 4, 5]
    resultado_media = media(numeros)
    print(resultado_media) 

    # Chamando a função media com parâmetros nomeados
    resultado_media = media(numeros=[1, 2, 3, 4, 5])
    print(resultado_media) 
    
```

## Docstrings

Docstrings são strings de documentação que descrevem o propósito e o funcionamento de uma função, classe ou módulo. Elas são escritas entre aspas triplas e podem ser acessadas usando a função `help()` ou o atributo `__doc__`.


:::tip PEP 257 
    PEP 257 é o guia de estilo para docstrings em Python. Ele fornece diretrizes sobre como escrever docstrings legíveis e consistentes. Algumas das principais recomendações incluem:
    - Usar aspas triplas para docstrings.
    - Colocar a docstring na primeira linha do corpo da função ou classe.
    - Usar a primeira linha como uma breve descrição da função ou classe.
    - Usar linhas em branco para separar a descrição da função ou classe de seus parâmetros e valores de retorno.
    - Usar o formato `:param` para descrever os parâmetros da função.
    - Usar o formato `:return` para descrever o valor de retorno da função.
    - Usar o formato `:raises` para descrever as exceções que a função pode gerar.
    - Usar o formato `:rtype` para descrever o tipo de retorno da função.

:::

:::tip PEP 8
    PEP 8 é o guia de estilo para Python. Ele fornece diretrizes sobre como escrever código Python legível e consistente. Algumas das principais recomendações incluem:
    - Usar 4 espaços para indentação.
    - Limitar o comprimento da linha a 79 caracteres.
    - Usar nomes de variáveis em `snake_case`.
    - Usar nomes de classes em `CamelCase`.
    - Usar espaços em branco em torno de operadores e após vírgulas.
    - Usar aspas simples ou duplas para strings, mas ser consistente.
    - Usar comentários para explicar o código.
    - Usar docstrings para documentar funções e classes.
    - Manter o código organizado e modular.
    - Evitar o uso de variáveis globais.
    - Usar `__init__.py` para marcar diretórios como pacotes.
    - Usar `__main__` para executar código de teste.

    Essas são apenas algumas das diretrizes. Para uma lista completa, consulte a [documentação oficial](https://www.python.org/dev/peps/pep-0008/).

:::

### Exemplos de docstrings

```python
    def soma(a: int, b: int) -> int:
        """
        Soma dois números inteiros.

        :param a: O primeiro número.
        :param b: O segundo número.
        :return: A soma dos dois números.
        """
        return a + b
```