# Desenvolvimento com Angular

## Instalação de dependências
Primeiro é necessário ter o <b>NodeJS</b>, após é necessário instalar no NPM o <b>Angular CLI</b> de forma global:

    npm install -g @angular/cli

Com ele instalado, crie uma pasta para o projeto e dentro dela utilize o seguinte comando para iniciação do projeto com o angular

    ng new nome-do-projeto

Através deste comando, será feita duas perguntas: Deseja criar um arquivo responsável pelo gerenciamento das rotas? e outra sobre qual o estilo deseja utilizar no projeto.

Projeto Criado! Agora dentro da pasta do projeto utilize o comando <code>ng serve</code> para executar a aplicação.

Certifique-se que está rodando no navegador. A porta local padrão é 4200

    http://localhost:4200

## Componentes
<br>

### <b>Criação do Componente</b>

<b>IMPORTANTE:</b> Sempre que criar um componente é recomendado desligar o servidor ng

Crie uma pasta <i>components</i> dentro do diretório <i>app</i>, e no terminal utilize o seguinte comando:

    ng generate component components/nome-do-componente

Temos a abreviação deste comando também:

    ng g c components/nome-do-componente

Dentro da pasta do componente você poderá editar o html(chamado <i>template</i>) e estilo dele.

### <b>Adicionando Componente a Página</b>

Para adicionar o componente a página, abra o arquivo <code>app.component.html</code>, nele delete todo código escrito por padrão e crie uma tag HTML com o nome do componente como o exemplo:

    <app-nome-do-componente></app-nome-do-componente>

Pronto, seu componente já pode ser visualizado, basta abrir novamente o servidor com o comando <code>ng serve</code>

### <b>Property Biding (Vinculação da Propriedade)</b>

Através deste método, podemos guardar as informações para enviá-las ao HTML. O responsável por esta lógica para criação, é o arquivo TS (chamado de <i>component</i>) e o arquivo HTML (chamado template) é o responsável pela demonstração do conteúdo.
<br>

Vamos a um exemplo, dentro do componente há o arquivo <code>nome-do-componente.component.ts</code>, abra o e escreva o seguinte código dentro de <code>export class</code>:

    export class CriarTextoComponent {
        texto = {
            id: '1',
            conteudo: 'Aprendendo Angular',
            autoria: 'John Doe',
            modelo: ''
        }

    }

Aqui guardamos os dados para a utilização. Agora dentro do componente acesse o seguinte arquivo <code>nome-do-componente.component.html</code>:
<br>

No arquivo, podemos acessar os dados do documento TS através de cochetes como por exemplo <code>[value] = "texto.conteudo"</code> ou também através de chaves <code>{{ texto.conteudo }}</code>

### <b>Event Binding (Vinculação do Evento)</b>

Este método ele cria dentro do template formas para chamar funções do TS. Para criar estes eventos, abra o arquivo do template HTML e dentro de uma tag adicione parênteses como o exemplo:

    <button (click)="salvar()" class="botao">Salvar</button>

Note que o editor de texto está apontando que há um erro neste código, pois dentro do arquivo TS não foi criada a função; Então crie a função no component TS:

    export class CriarPensamentoComponent {
        salvar() {
            alert("Salvo");
        }
    }

### <b>Two Way Data Binding (Fluxo de Dados Bidirecional)</b>

Caso queira utilizar um campo tanto para receber dados como também enviá-los, utilize uma diretiva <b>ngModel</b>.

Diretivas são classes que conseguem modificar elementos na aplicação Angular.

Para utilizar o ngModel, observe o exemplo dentro de uma tag HTML do template:

    <input
        type="text"
        placeholder="Digite um atributo"
        [(ngModel)]="item.atributo"
    >

<u>OBS.:</u> Em caso do editor demonstrar erro na linha do ngModel, entre no arquivo `app.module.ts` e dentro do array de <i>imports</i> adicione a palavra FormsModule

    imports: [
        BrowserModule,
        AppRoutingModule,
        FormsModule
    ],

e se o seu editor não adicionou a importação automaticamente adicione essa linha no topo do documento:

    import { FormsModule } from '@angular/forms';

### <b>Arrays e Loopings - *ngFor</b>
Para a utilização de loopings no Angular utilize a diretiva `*ngFor`, vamos criar um componente pai:

    <div *ngFor="let elemento of listaElementos">
        <componente></componente>
    </div>

Primeiro, crie um objeto para o `<componente>` para ele ser a base para outros:

    @Input() objetoFilhoExemplo = {
        conteudo: 'eu sou o filho',
        dia: '01/01/2000'
    }

    // O @Input() serve para receber informações do componente pai

<u>Obs.:</u> Certifique-se que a importação do @Input foi realizada.

Agora precisamos adicionar uma <i>Property Binding</i> no laço ngFor:

    <div *ngFor="let elemento of listaElementos">
        <componente [objetoFilhoExemplo]="elemento"></componente>
    </div>

Agora temos a base para a criação da lista para o looping funcionar. Como nenhuma lista foi declarada, a div com o array não aparecerá. Para resolver isso, primeiramente, crie uma lista dentro do TS do componente pai:

    listaElementos = [
        {
            conteudo: 'eu sou o elemento 1',
            dia: '31/12/2022'   
        }
        {
            conteudo: 'eu sou o elemento 2',
            dia: '01/02/2023'   
        }
        {
            conteudo: 'eu sou o elemento 3',
            dia: '01/04/2023'   
        }
    ]

### <b>IF e ELSE - *ngIf</b>
Para o exemplo de condicionais, vamos fazer com que uma div apareça ou não:

    <div class="albumFotos" *ngIf="album.length > 0, else semFoto">
        <!-- Album de fotos -->
    </div>
    <ng-template>
        <div class="sem-fotos" #semFoto>
            <p>Não há fotos no Álbum!</p>
        </div>
    </ng-template>

Neste código criamos uma div em que nela há a condição que um array `album` deve ser maior que 0, caso não haja fotos utilizamos o else e é carregada no lugar a tag `<ng-template>`.

### <b>Estilos condicionais - ngClass</b>
No css vamos criar duas classes:

    .vermelho {
        background-color: red;
    }
    .azul {
        background-color: blue;
    }

Agora no template, para criar uma detecção será inserido o `ngClass` na tag HTML:

    <div class="container" [ngClass]="adicionaCor()">

No arquivo component TS, vamos criar uma condicional para retornar a cor para div:

    adicionaCor(): string {
        if(this.escola.nota > 6) {
            return 'azul';
        } else {
            return 'vermelho';
        }
    }

## Rotas
<br>

### <b>Criando e Configurando Rotas</b>

Para criação de rotas de forma dinâmica adicione no `app.component.html` a seguinte tag:

    <router-outlet></router-outlet>

Agora, abra o arquivo `app-routing.module.ts` e adicione o seguinte código dentro do array de Routes:

    const routes: Routes = [
    {
        path: '', // página inicial
        pathMatch: 'full',
        redirectTo: 'login' // redireciona para localhost:4200/login
    },
    {
        path: 'login',
        component: LoginComponent
    },
    {
        path: 'cadastro',
        component: CadastroComponent
    }
    ];

Sempre que criamos um path vazio, é necessário criar a propriedade pathMatch. Esta propriedade possui dois valores `prefix` e `full`; Utilizando `prefix` somente o endereço inicial (antes da barra) será considerado; Utilizando `full` toda a URL é considerada.


<u>OBS.:</u> Não esqueça de verificar se os componentes foram importados no arquivo.

### <b>Criando Links - routerLink</b>

Para adicionar um link ao seu componente, basta adicionar a diretiva `routerLink`:

    <button routerLink="/cadastro">Faça seu cadastro</button>
