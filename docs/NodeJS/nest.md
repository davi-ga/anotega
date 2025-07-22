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

#### Retorno



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


## Decorators

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