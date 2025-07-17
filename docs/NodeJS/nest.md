---
sidebar_position: 1
---

# NestJS

O NestJS é um framework para construir aplicações Node.js eficientes, confiáveis e escaláveis. Ele é construído com TypeScript e combina elementos de programação orientada a objetos, programação funcional e programação reativa. É um framework opinado que segue o padrão de arquitetura MVC (Model-View-Controller) e é inspirado em frameworks como Angular.

 
 ## Inicialização

Para iniciar um projeto NestJS, você pode usar o CLI do NestJS. Primeiro, instale o CLI globalmente:
```bash
npm install -g @nestjs/cli
```

Em seguida, crie um novo projeto:
```bash
nest new my-nest-app
```

Isso criará uma estrutura de diretórios básica para o seu projeto NestJS.

## Estrutura do Projeto

A estrutura básica de um projeto NestJS é a seguinte:

```
my-nest-app/
├── node_modules/
├── src/
│   ├── app.controller.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   └── main.ts
├── test/
│   └── app.e2e-spec.ts
├── .eslintrc.js
├── .prettierrc
├── package.json
├── package-lock.json
├── tsconfig.json
├── tsconfig.build.json
└── nest-cli.json
```
- `node_modules/` contém as dependências do projeto.
- `src/` contém o código-fonte da aplicação.
    - `app.controller.ts` define os controladores da aplicação.
    - `app.module.ts` é o módulo raiz da aplicação.
    - `app.service.ts` contém a lógica de negócios.
    - `main.ts` é o ponto de entrada da aplicação.
- `test/` contém os testes da aplicação.
  - `app.e2e-spec.ts` é um exemplo de teste de ponta a ponta.
- `.eslintrc.js` é o arquivo de configuração do ESLint(F).
- `.prettierrc` é o arquivo de configuração do Prettier.
- `package.json` contém as dependências e scripts do projeto.
- `package-lock.json` é o arquivo de bloqueio de dependências do NPM.
- `tsconfig.json` é o arquivo de configuração do TypeScript.
- `tsconfig.build.json` é o arquivo de configuração do TypeScript para construção.
- `nest-cli.json` é o arquivo de configuração do CLI do NestJS.

## Conceitos Básicos

### Main

O ponto de entrada da aplicação é o arquivo `main.ts`, onde o aplicativo NestJS é criado e iniciado. Aqui, você pode configurar o servidor, middleware e outras funcionalidades.

```typescript title="main.ts"
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

### Modules
Os módulos são a base da estrutura do NestJS. Cada módulo é uma classe anotada com o decorador `@Module()`, que define os componentes que pertencem a esse módulo, como controladores e provedores.

Serve para conectar diferentes partes da aplicação, como controladores, serviços e outros módulos. Cada módulo é uma classe anotada com o decorador `@Module()`.

```typescript title="app.module.ts"
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

### Controllers
Os controladores são responsáveis por lidar com as requisições HTTP. Eles são anotados com o decorador `@Controller()` e definem rotas para os endpoints da aplicação.

Possui métodos que respondem a requisições HTTP e são anotados com decoradores como `@Get()`, `@Post()`, `@Put()`, etc. Esses métodos recebem os dados da requisição e retornam uma resposta.

```typescript title="app.controller.ts"
import { Controller, Get } from '@nestjs/common';

@Controller('/')
export class AppController {
    constructor(private readonly appService: AppService) {}

    @Get()
    getHello(): string {
        return this.appService.getHello();
    }
}
```

:::tip Rotas
    As rotas são definidas nos controladores e podem ser personalizadas com parâmetros, consultas e outras opções.

    ```typescript title="app.controller.ts"
    @Controller('users')
    export class UsersController {
        @Get(':id')
        getUser(@Param('id') id: string): string {
            return `User ID: ${id}`;
        }

        @Post('create')
        createUser(@Body() createUserDto: CreateUserDto): string {
            return `User created with name: ${createUserDto.name}`;
        }
    }


    ```
:::

### Services

Os serviços contêm a lógica de negócios da aplicação. Eles são anotados com o decorador `@Injectable()` e podem ser injetados em controladores ou outros serviços.

```typescript title="app.service.ts"

import { Injectable } from '@nestjs/common';
@Injectable()
export class AppService {
    getHello(): string {
        return 'Hello World!';
    }
    }
```

## Data Objects (DTOs)

Os Data Transfer Objects (DTOs) são usados para definir a estrutura dos dados que serão enviados e recebidos nas requisições. Eles são anotados com o decorador `@Dto()` e podem incluir validações usando decoradores do pacote `class-validator`.

```typescript title="create-user.dto.ts"
import { IsString, IsInt } from 'class-validator';
export class CreateUserDto {
    @IsString()
    name: string;
    @IsInt()
    age: number;
}
```   

:::tip Validações
    As validações são aplicadas automaticamente quando os DTOs são usados nas rotas. Se os dados não atenderem aos critérios definidos, uma exceção será lançada.
:::

## Inversão de Dependência (DI)

O NestJS utiliza o padrão de Inversão de Dependência (DI) para gerenciar a criação e injeção de dependências. Isso permite que os serviços sejam facilmente testáveis e reutilizáveis.

Os serviços podem ser injetados em controladores ou outros serviços usando o construtor. O NestJS cuida da criação e injeção das instâncias necessárias.

```typescript title="app.controller.ts"
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';
@Controller('/')
export class AppController {
    constructor(private readonly appService: AppService) {}
    @Get()
    getHello(): string {
        return this.appService.getHello();
    }
}
``` 

Nesse exemplo, o `AppService` é injetado no `AppController`, permitindo que o controlador utilize os métodos do serviço.

## Injeção de Dependências

A injeção de dependências é uma característica fundamental do NestJS, permitindo que você injete serviços e outros módulos em seus controladores e serviços. Isso promove a reutilização de código e facilita os testes.

Você pode injetar serviços usando o construtor do controlador ou serviço. O NestJS resolve automaticamente as dependências necessárias.

```typescript title="app.module.ts"
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module'; 

@Module({
  imports: [UsersModule], // Importando o módulo de usuários
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

## DTOs (Data Transfer Objects)

Os DTOs são usados para definir a estrutura dos dados que serão enviados e recebidos nas requisições. Eles ajudam a validar e transformar os dados antes de serem processados pelos controladores ou serviços.

```typescript title="create-user.dto.ts"
export interface CreateUserDto {
    name: string;
    age: number;
}
```

### Validações

As validações podem ser aplicadas aos DTOs usando o pacote `class-validator`. Isso permite que você defina regras de validação para os campos dos DTOs, garantindo que os dados recebidos estejam corretos.

```typescript title="create-user.dto.ts"
import { IsString, IsInt } from 'class-validator';
export class CreateUserDto {
    @IsString()
    name: string;
    @IsInt()
    age: number;
}
```

:::warning 
  Decorators de validação do class-validator só funcionam em classes, não em interfaces. Portanto, é recomendado usar classes para DTOs quando você precisar de validações.
:::