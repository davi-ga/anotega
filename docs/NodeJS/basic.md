---
sidebar_position: 1
---

# NodeJS

O NodeJS é um *ambiente de execução JavaScript* do lado do servidor, que permite executar código JavaScript fora de um navegador. Ele é construído sobre o motor V8 do Google Chrome e é amplamente utilizado para criar aplicações web escaláveis e de alto desempenho.

## Gerenciamento de Pacotes

São ferramentas que *automatizam* o processo de instalação, atualização e remoção de bibliotecas e dependências em projetos Node.js. No contexto do Node.JS, esses pacotes geralmente contêm bibliotecas, frameworks e utilitários que facilitam o desenvolvimento de aplicações.

Scripts são comandos definidos no arquivo `package.json` que podem ser executados usando o comando `npm<qualquer-outro-gerenciador> run <script-name>`. Esses scripts são úteis para automatizar tarefas comuns, como testes, construção de projetos e execução de servidores de desenvolvimento.

```json title="package.json"
{
  "scripts": {
    "start": "node index.js",
    "test": "jest",
    "build": "tsc",
    "lint": "eslint .",
    "format": "prettier --write ."
  },
}
```

### NPM

O NPM é o **gerenciador de pacotes padrão** do Node.js, que permite instalar e gerenciar pacotes de terceiros. Ele é amplamente utilizado na comunidade Node.js e possui um **vasto repositório de pacotes** disponíveis. Permite configurar **registries de pacotes personalizados**, o que é útil para empresas que desejam manter seus próprios pacotes privados ou usar pacotes de terceiros de fontes específicas.

### Yarn

O Yarn é um gerenciador de pacotes alternativo ao NPM, **criado pelo Facebook**. Ele oferece uma série de melhorias em relação ao NPM, como:
- **Instalação mais rápida** de pacotes usando cache
- **Garantia de determinismo** na instalação de dependências 
- **Suporte a workspaces** para gerenciar múltiplos pacotes em um único repositório


### PNPM

O PNPM é um gerenciador de pacotes que se destaca por sua **eficiência no uso de espaço em disco**. Ele utiliza um **sistema de links simbólicos** para compartilhar dependências entre projetos, o que **reduz significativamente o espaço** ocupado por pacotes duplicados. Também oferece **isolamento de dependências**, garantindo que cada projeto tenha suas próprias versões de pacotes, evitando conflitos.

### BUN

O Bun é um gerenciador de pacotes e runtime JavaScript que se destaca por sua **velocidade e eficiência**. Ele é projetado para ser uma **alternativa mais rápida** ao NPM e Yarn, oferecendo **tempos de instalação significativamente menores**. O Bun também inclui um **bundler integrado**, o que facilita a criação de aplicações web otimizadas.

![comparacao](image.png)

## TypeScript

O TypeScript é um superconjunto do JavaScript que adiciona tipagem estática e outros recursos avançados à linguagem. Ele é amplamente utilizado no desenvolvimento de aplicações Node.js, pois ajuda a detectar erros em tempo de compilação e melhora a legibilidade do código.

É uma ferramenta poderosa para desenvolvedores que desejam criar aplicações mais robustas e manuteníveis.

### Strict Mode


### Configuração do TypeScript

Para configurar o TypeScript em um projeto Node.js, você precisa criar um arquivo `tsconfig.json` na raiz do seu projeto. Este arquivo define as opções de compilação do TypeScript, como o diretório de saída, o alvo da compilação e outras configurações.

```json title="tsconfig.json"
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "**/*.spec.ts"]
}
```

O `target` especifica a versão do ECMAScript para a qual o código será compilado, enquanto o `module` define o sistema de módulos a ser usado. O `outDir` é o diretório onde os arquivos compilados serão colocados, e o `rootDir` é o diretório raiz do código-fonte, `strict` ativa o modo estrito, `esModuleInterop` permite a interoperabilidade com módulos ES, e `skipLibCheck` ignora a verificação de tipos em arquivos de declaração de biblioteca, enquanto `include` e `exclude` definem quais arquivos devem ser incluídos ou excluídos da compilação.

:::tip Strict Mode

O modo estrito do TypeScript é uma configuração que ativa verificações adicionais de tipo e segurança no código. Ele ajuda a evitar erros comuns e melhora a qualidade do código. Para ativar o modo estrito, adicione `"strict": true` ao seu arquivo `tsconfig.json`.

```json title="tsconfig.json"
{
  "compilerOptions": {
    "strict": true,
    // outras opções...
  }
}
```

:::

### Tipos Básicos

Os tipos básicos do TypeScript incluem `number`, `string`, `boolean`, `null`, `undefined`, `any`, `void` e `never`. Esses tipos são usados para definir variáveis, parâmetros de função e valores de retorno.

```typescript
let idade: number = 30;
let nome: string = "João";
let ativo: boolean = true;
let nulo: null = null;
let indefinido: undefined = undefined;
let qualquer: any = "pode ser qualquer coisa";

function exibirMensagem(): void {
  console.log("Olá, TypeScript!");
}

function nuncaRetorna(): never {
  throw new Error("Esta função nunca retorna");
}
```
:::tip Inferência de Tipos

O TypeScript possui um sistema de *inferência de tipos* que permite que o compilador deduza automaticamente o tipo de uma variável com base no valor atribuído a ela. Isso significa que você não precisa declarar explicitamente o tipo em muitos casos, tornando o código mais conciso.

```typescript
let idade = 30; // O TypeScript infere que idade é do tipo number
let nome = "João"; // O TypeScript infere que nome é do tipo string
```
:::

#### Template Strings

As template strings são uma forma de criar strings multilinha e interpolar expressões dentro de strings. Elas são definidas usando crases (`` ` ``) em vez de aspas simples ou duplas.

```typescript
let nome = "João";
let mensagem = `Olá, ${nome}! Bem-vindo ao TypeScript.`;
console.log(mensagem);
```

### Tipos Avançados

Os tipos avançados do TypeScript incluem `enum`, `tuple`, `union`, `intersection`, `literal types` e `type aliases`. Esses tipos permitem criar estruturas de dados mais complexas e flexíveis.

#### Enumerações

As enumerações são um tipo especial que permite definir um conjunto de valores nomeados. Elas são úteis para representar estados ou categorias fixas em seu código.

```typescript
enum Cor {
  Vermelho,
  Verde,
  Azul
}

enum Status {
  Ativo = "ativo",
  Inativo = "inativo"
}
```

#### Arrays

Os arrays são coleções ordenadas de elementos do mesmo tipo. No TypeScript, você pode definir o tipo dos elementos de um array usando a sintaxe `tipo[]` ou `Array<tipo>`.

```typescript
let numeros: number[] = [1, 2, 3, 4, 5];
let nomes: Array<string> = ["João", "Maria", "Pedro"];
```

### Funções

As funções no TypeScript podem ter tipos de parâmetros e tipos de retorno definidos. Isso ajuda a garantir que as funções sejam chamadas com os tipos corretos de argumentos e que retornem os tipos esperados.

```typescript
function somar(a: number, b: number): number {
  return a + b;
}

const add = (a: number, b: number): number => {
  return a + b;
};

```

#### Rest Params

Os parâmetros rest permitem que uma função aceite um número variável de argumentos como um array. Isso é útil quando você não sabe quantos argumentos serão passados para a função.

```typescript
function somarTudo(...numeros: number[]): number {
  return numeros.reduce((total, num) => total + num, 0);
} 
```

### Classes

As classes no TypeScript são uma forma de definir objetos com propriedades e métodos. Elas suportam herança, encapsulamento e polimorfismo, permitindo criar estruturas de dados complexas e reutilizáveis.

```typescript
class Pessoa {
  nome: string;
  idade: number;
  constructor(nome: string, idade: number) {
    this.nome = nome;
    this.idade = idade;
  }
}   
```

#### Construtores

Os construtores são métodos especiais que são chamados quando uma instância de uma classe é criada. Eles são usados para inicializar as propriedades da classe.

```typescript
class Pessoa {
  nome: string;
  idade: number;
  constructor(nome: string, idade: number) {
    this.nome = nome;
    this.idade = idade;
  }
}
```

#### Visibilidade

As visibilidades em TypeScript controlam o acesso às propriedades e métodos de uma classe. Existem três modificadores de visibilidade: `public`, `private` e `protected`.

```typescript
class Animal {
  public nome: string;
  private idade: number;
  protected especie: string;

  constructor(nome: string, idade: number, especie: string) {
    this.nome = nome;
    this.idade = idade;
    this.especie = especie;
  }

```

`public` permite acesso de qualquer lugar, `private` restringe o acesso apenas à própria classe, e `protected` permite acesso à própria classe e suas subclasses.

#### Herança

A herança permite que uma classe herde propriedades e métodos de outra classe. Isso promove a reutilização de código e a criação de hierarquias de classes.

```typescript
class Animal {
  nome: string;
  constructor(nome: string) {
    this.nome = nome;
  }
} 

class Cachorro extends Animal {
  latir(): void {
    console.log(`${this.nome} está latindo!`);
  }
} 
```

### Interfaces

As interfaces são uma forma de definir contratos para objetos e classes. Elas permitem especificar quais propriedades e métodos um objeto deve ter, sem implementar a lógica.

```typescript
interface PessoaInterface {
  nome: string;
  idade: number;

  falar(): void;
}

class Estudante implements PessoaInterface {
  nome: string;
  idade: number;
  constructor(nome: string, idade: number) {
    this.nome = nome;
    this.idade = idade;
  }
  falar(): void {
    console.log(`Meu nome é ${this.nome} e tenho ${this.idade} anos.`);
  }
}
```

### Extra

#### Omit

Omit é um utilitário do TypeScript que permite criar um novo tipo removendo uma ou mais propriedades de um tipo existente. Isso é útil quando você deseja criar um tipo baseado em outro, mas sem algumas propriedades específicas.

```typescript
interface Usuario {
  id: number;
  nome: string;
  email: string;
}   

type UsuarioSemEmail = Omit<Usuario, 'email'>;
const usuario: UsuarioSemEmail = {
  id: 1,
  nome: 'João',
  // email: 'joao@example.com'

  // A propriedade 'email' foi omitida

};
```
