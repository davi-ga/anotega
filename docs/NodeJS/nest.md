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


#### Application Context

O contexto da aplicação é o ambiente onde o NestJS executa. Ele é criado quando você chama `NestFactory.createApplicationContext(AppModule)`. O contexto contém informações sobre os módulos, controladores e provedores registrados na aplicação.

```typescript title="main.ts"
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
async function bootstrap() {
  const app = await NestFactory.createApplicationContext(AppModule);
  await app.listen(3000);
}
bootstrap();
```

:::tip Contexto da Aplicação
    O contexto da aplicação é útil para acessar serviços e módulos fora do ciclo de vida de uma requisição HTTP, como em tarefas agendadas ou scripts de inicialização.
:::

#### Swagger

Para documentar sua API, você pode usar o Swagger. O NestJS possui integração nativa com o Swagger, permitindo que você gere documentação interativa para sua API.
```typescript title="main.ts"
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('API Example')
    .setDescription('API description')
    .setVersion('1.0')
    .build();
  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('docs', app, document);

  await app.listen(3000);
}
bootstrap();
```

:::tip Swagger
    A documentação Swagger estará disponível em `http://localhost:3000/docs` após iniciar a aplicação.
:::

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

#### Repository

Os Repositórios são responsáveis pela interação com a camada de persistência de dados. Eles encapsulam a lógica de acesso a dados e fornecem uma interface para os serviços. No NestJS, você pode criar Repositórios usando o padrão de projeto Repository.

```typescript title="user.repository.ts"
import { EntityRepository, Repository } from 'typeorm';
import { User } from './user.entity';

@EntityRepository(User)
export class UserRepository extends Repository<User> {
    // Métodos personalizados para acessar dados de usuários
}
```

Geralmente usa-se dentro de um Service e é uma melhoria de segundo plano

### Decorators

Os Decorators são uma parte fundamental do NestJS e do TypeScript. Eles são usados para adicionar metadados às classes, métodos, propriedades e parâmetros. No NestJS, os decoradores são amplamente utilizados para definir controladores, rotas, injeção de dependências e muito mais.

Eles são funções que podem ser aplicadas a classes, métodos, propriedades ou parâmetros para modificar seu comportamento ou adicionar metadados. No NestJS, os decoradores são usados para definir controladores, rotas, injeção de dependências e muito mais.

```typescript title="example.decorator.ts"
import { SetMetadata } from '@nestjs/common';
export const Roles = (...roles: string[]) => SetMetadata('roles', roles);
```

```typescript title="example.controller.ts"
import { Controller, Get, UseGuards } from '@nestjs/common';
import { Roles } from './example.decorator';
import { RolesGuard } from './roles.guard';
@Controller('example')
export class ExampleController {
    @Get()
    @Roles('admin')
    @UseGuards(RolesGuard)
    getExample() {
        return 'This is an example route';
    }
}

```



## Inversão de Dependência

O NestJS segue o princípio da Inversão de Dependência (DIP - Dependency Inversion Principle), que é um dos princípios SOLID. Este princípio estabelece que:

- Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.
- Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.

No NestJS, isso significa que os controladores dependem de abstrações (interfaces) dos serviços, não de suas implementações concretas. Isso torna o código mais flexível, testável e facilita a manutenção.

```typescript title="user.service.interface.ts"
export interface IUserService {
    getUser(id: string): Promise<User>;
    createUser(userData: CreateUserDto): Promise<User>;
}
```

```typescript title="app.controller.ts"
import { Controller, Get } from '@nestjs/common';
import { IUserService } from './interfaces/user.service.interface';

@Controller('/')
export class AppController {
    constructor(private readonly userService: IUserService) {}
    
    @Get()
    getUsers(): Promise<User[]> {
        return this.userService.getAllUsers();
    }
}
``` 

Nesse exemplo, o `AppService` é injetado no `AppController`, permitindo que o controlador utilize os métodos do serviço.

## Injeção de Dependências

A Injeção de Dependências (DI - Dependency Injection) é a técnica utilizada pelo NestJS para implementar o princípio da Inversão de Dependência. É o mecanismo que permite fornecer as dependências necessárias para uma classe sem que ela precise criá-las diretamente.

O NestJS possui um container de IoC (Inversion of Control) que gerencia automaticamente a criação e injeção das instâncias dos serviços. Isso promove:

- **Baixo acoplamento**: Classes não dependem de implementações concretas
- **Facilidade de testes**: Dependências podem ser facilmente "mockadas"
- **Reutilização de código**: Serviços podem ser compartilhados entre diferentes módulos

Você pode injetar serviços usando o construtor do controlador ou serviço. O NestJS resolve automaticamente as dependências necessárias.

```typescript title="app.module.ts"
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module'; 

@Module({
  imports: [UsersModule],
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


## JWT

O JWT (JSON Web Token) é um padrão aberto (RFC 7519) que define um formato compacto e autocontido para transmitir informações entre partes como um objeto JSON. No NestJS, você pode usar o pacote `@nestjs/jwt` para implementar autenticação baseada em JWT.

Ele é amplamente utilizado para autenticação e autorização em aplicações web. O JWT é composto por três partes: header, payload e signature. Ele permite que você autentique usuários de forma segura e escalável.
-- **Header**: Contém informações sobre o tipo de token e o algoritmo de assinatura.
-- **Payload**: Contém as informações do usuário e outras reivindicações (claims).
-- **Signature**: É usada para verificar a integridade do token e garantir que ele não foi alterado.

```typescript title="jwt.strategy.ts"
import { Injectable } from '@nestjs/common';
import { PassportStrategy } from '@nestjs/passport';
import { ExtractJwt, Strategy } from 'passport-jwt';
import { JwtPayload } from './jwt-payload.interface';

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
    constructor() {
        super({
            jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
            ignoreExpiration: false,
            secretOrKey: 'your_jwt_secret',
        });
    }

    async validate(payload: JwtPayload) {
        return { userId: payload.sub, username: payload.username };
    }
}
```

### Guards

Os Guards são usados para proteger rotas e controlar o acesso a elas. Eles são classes que implementam a interface `CanActivate` e podem ser usados para verificar se uma requisição deve ser processada ou não.

Eles são executados antes que a requisição seja manipulada pelo controlador e podem ser usados para autenticação, autorização ou outras verificações de segurança.

```typescript title="auth.guard.ts"
import { Injectable } from '@nestjs/common';
import { CanActivate, ExecutionContext } from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';

@Injectable()
export class AuthGuard implements CanActivate {
    constructor(private readonly jwtService: JwtService) {}

    canActivate(context: ExecutionContext): boolean {
        const request = context.switchToHttp().getRequest();
        const token = request.headers.authorization?.split(' ')[1];
        if (!token) return false;

        try {
            const payload = this.jwtService.verify(token);
            request.user = payload;
            return true;
        } catch (error) {
            return false;
        }
    }
}

```



## Pipes

Os Pipes são usados para transformar e validar os dados das requisições antes que eles sejam processados pelos controladores. Eles podem ser usados para aplicar validações, transformações ou manipulações nos dados recebidos.

Eles são classes que implementam a interface `PipeTransform` e podem ser usados para transformar ou validar os dados das requisições antes que eles sejam processados pelos controladores.

São executados após o middleware e antes do controlador.


### Parse

Os Pipes de Parse são usados para transformar os dados das requisições em tipos específicos. Eles podem ser usados para converter strings em números, booleans ou outros tipos de dados.


#### Built-in Pipes

O NestJS fornece vários Pipes embutidos que podem ser usados para validação e transformação de dados. Alguns dos Pipes embutidos mais comuns incluem:

```typescript title="example.controller.ts"         
    import { Controller, Get, Param, UsePipes } from '@nestjs/common';
    import { ParseIntPipe } from './parse-int.pipe';
    @Controller('example')
    export class ExampleController {
        @Get(':id')
        getExample(@Param('id',ParseIntPipe) id: number) {
            return `Example with ID: ${id}`;
        }
    }
```
### Validation Pipes

Os Validation Pipes são usados para validar os dados das requisições antes que eles sejam processados pelos controladores. Eles podem ser usados para aplicar regras de validação, como verificar se um campo é obrigatório, se um valor está dentro de um intervalo ou se um campo é do tipo correto.

```typescript title="example.controller.ts"
import { Controller, Post, Body, UsePipes } from '@nestjs/common';
import { ValidationPipe } from './validation.pipe';
@Controller('example')
export class ExampleController {
    @Post()
    createExample(@Body(new ValidationPipe()) createExampleDto: CreateExampleDto) {
        return `Example created with data: ${JSON.stringify(createExampleDto)}`;
    }
}
```

## Prisma   

O Prisma é um ORM (Object-Relational Mapping) moderno e poderoso para Node.js e TypeScript. Ele facilita a interação com bancos de dados relacionais, permitindo que você escreva consultas de forma intuitiva e segura.

Para usar o Prisma no NestJS, você precisa instalar o pacote `@nestjs/prisma` e configurar o Prisma Client.

```bash
npm install @nestjs/prisma prisma
```

Em seguida, você pode criar um módulo Prisma e configurar o Prisma Client.

```typescript title="prisma.module.ts"
import { Module } from '@nestjs/common';    
import { PrismaService } from './prisma.service';
@Module({
  providers: [PrismaService],
  exports: [PrismaService],
})
export class PrismaModule {}
```

```typescript title="prisma.service.ts"
import { Injectable } from '@nestjs/common';
import { PrismaClient } from '@prisma/client';
@Injectable()
export class PrismaService extends PrismaClient {
    constructor() {
        super();
    }
}
}
```

Com isso é possível injetar o `PrismaService` em outros serviços ou controladores e usar o Prisma Client para interagir com o banco de dados.

```typescript title="user.service.ts"
import { Injectable } from '@nestjs/common';
import { PrismaService } from './prisma.service';
@Injectable()
export class UserService {
    constructor(private readonly prisma: PrismaService) {}
    async getUser(id: number) {
        return this.prisma.user.findUnique({ where: { id } });
    }
    async createUser(data: CreateUserDto) {

        return this.prisma.user.create({ data });
    }
}
``` 

### Queries

As consultas no Prisma são feitas usando o Prisma Client, que fornece métodos para interagir com o banco de dados. Você pode usar métodos como `findUnique`, `findMany`, `create`, `update` e `delete` para realizar operações CRUD.


#### Joins

Para realizar joins com o Prisma, você pode usar a opção `include` nas consultas. Isso permite que você busque dados relacionados de outras tabelas.

```typescript title="user.service.ts"
async getUserWithPosts(id: number) {
    return this.prisma.user.findUnique({
        where: { id },
        include: { posts: true }
    });
}
```

O uso do `omit` permite que você exclua campos específicos do resultado da consulta. Isso é útil quando você não precisa de todos os campos de um registro.

```typescript title="user.service.ts"
async getUserWithPosts(id: number) {
    return this.prisma.user.findUnique({
        where: { id },
        include: {
            posts: {
                omit: {
                    createdAt: true,
            },
        },
    });
}
```

O uso do `select` permite que você selecione apenas os campos específicos que deseja retornar na consulta. Isso é útil para otimizar o desempenho e reduzir a quantidade de dados retornados.

```typescript title="user.service.ts"
async getUserWithSelectedFields(id: number) {
    return this.prisma.user.findUnique({
        where: { id },
        select: {
            name: true,
            email: true,
            posts: {
                select: {
                    title: true,
                    content: true,
                },
            },
        },
    });
}
```

#### Create

Para criar registros no Prisma, você pode usar o método `create`. Ele permite que você especifique os dados do novo registro.

```typescript title="user.service.ts"
async createUser(data: CreateUserDto) {
    return this.prisma.user.create({
        data: {
            name: data.name,
            email: data.email,
        },
    });
}
```

É possível fazer create aninhado, ou seja, criar registros relacionados em uma única consulta.

```typescript title="user.service.ts"
async createUserWithPosts(data: CreateUserDto) {
    return this.prisma.user.create({
        data: {
            name: data.name,
            posts: {
                create: data.posts.map(post => ({
                    title: post.title,   
                    content: post.content,
                })),
            },
        },
    });
}
```

#### Update

Para atualizar registros no Prisma, você pode usar o método `update`. Ele permite que você especifique o registro a ser atualizado e os novos dados.

```typescript title="user.service.ts"
async updateUser(id: number, data: UpdateUserDto) {
    return this.prisma.user.update({
        where: { id },
        data,
    });
}
```

É possível fazer update aninhado, ou seja, atualizar registros relacionados em uma única consulta.

```typescript title="user.service.ts"
async updateUserWithPosts(id: number, data: UpdateUserDto) {
    return this.prisma.user.update({
        where: { id },
        data: {
            name: data.name,
            posts: {
                update: data.posts.map(post => ({
                    where: { id: post.id },
                    data: { title: post.title, content: post.content },
                })),
            },
        },
    });
}
```



### Implements

Os `implements` são usados para garantir que uma classe siga uma interface específica. No NestJS, você pode usar `implements` para definir contratos para serviços, controladores ou outros componentes.

```typescript title="user.service.ts"
import { Injectable } from '@nestjs/common';
import { IUserService } from './interfaces/user.service.interface';

@Injectable()
export class UserService implements IUserService {
    // Implementação dos métodos da interface IUserService
}
```

## Parse