# Backend - JSON Server e realização do CRUD

## Iniciando e criando arquivos necessários

Inicialmente, crie uma pasta chamada <i>backend</i> dentro da sua aplicação. Após inicie o npm nela:

    npm init -y

Precisaremos instalar as seguintes dependências: JSON Server

    npm install json-server

Crie um arquivo chamado `db.json`, dentro dele terá todos os endpoints da aplicação.

    {
      "lista-objetos": [
        {
          "id": 1,
          "content": "lorem ipsum dolor sit amet",
          "autor": "John Doe"
        },
        {
          "id": 2,
          "content": "lorem lorem ipsum dolor sit amet",
          "autor": "John Joe"
        },
        {
          "id": 3,
          "content": "lorem ipsum dolor ipsum sit amet",
          "autor": "Jone Does"
        }
      ]
    }

Neste código temos um exemplo de dados para praticarmos<br/>

Crie em seu `package.json` o seguinte código dentro de `"scripts"`:

    "scripts": {
      "start": "json-server --watch db.json --port 3000"
    }

Aqui setamos a forma para chamar os dados do json, sempre que iniciar sua aplicação inicie junto o backend com `npm start`.

### <b> Criação de Interface Typescript </b>

Para a padronização dos dados que chegarem ao nosso `db.json`, temos que criar um arquivo chamado `interface.ts` no diretório: `/app/components/nome-do-componente/interface.ts` :

    export interface Objeto {
      id: number
      content: string
      autor: string
    }
