# Projeto Área de Transferência

## Finalidade:
Este aplicativo oferece frases para o operador de reservas da Pousada

## Objetivos do projeto para esta aula
- Criar projetos backend e frontend
- Salvar os projeto no Github em monorepo
- Montar o visual estático do front end

## Checklist

### Passo: preparação

#### Dica: extensões do VS Code

#### Conferir Node (16 LTS) e Yarn

[Guia de instalação das ferramentas](https://github.com/devsuperior/sds-dsmovie/tree/main/_instalacao)

```bash
node -v
yarn -v
```

Caso precise instalar o Yarn, faça o comando:

```
npm install --global yarn
```

#### Design Figma
https://www.figma.com/file/b8W4zkYaTlvGk7eyAZ7Yfr/%C3%81rea-de-Transferencia?node-id=0%3A1

### Passo: criar projeto ReactJS

- ATENÇÃO: esta será a estrutura de pastas que vamos criar:
- 

![pastas](https://github.com/mauricioqvp/assets/blob/main/assets/img/pastas.png)

![pastas](https://github.com/mauricioqvp/assets/blob/main/assets/img/pastas.png)


yarn create react-app frontend --template typescript
```
OU:
```
npx create-react-app frontend --template typescript
```

IMPORTANTE: deletar subpasta .git
- *Lembrete: ver extensões e arquivos ocultos*

### Passo: criar projeto Spring Boot

- Criar projeto Spring Boot no `Spring Initializr` com as seguintes dependências:
  - Web
  - JPA
  - H2
  - Postgres
  - Security

- Ajuste no arquivo pom.xml:

```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-resources-plugin</artifactId>
	<version>3.1.0</version>
</plugin>
```

  - Botão direito no projeto -> Maven -> Update project (force update)

### Passo: salvar primeira versão no Github

[Playlist de introdução e configuração do Git/Github](https://www.youtube.com/watch?v=KLG-jC1fh28&list=PLNuUvBZGBA8nDTr8QRMgoT_l3XNt_BbWj)

```bash
git config --global user.name <seu nome>
git config --global user.email <seu email>

git init

git add .

git commit -m "Project created"

git remote ...
```

```bash
git status

git remote -v

git branch -M main

git push -u origin main
```

### Passo: "limpar" o projeto ReactJS

- Deletar arquivos não usados

- **COMMIT: Project clean**

### Passo: adicionar Bootstrap e CSS ao projeto
- Bootstrap
```
yarn add bootstrap@5.1.3
```

- Arquivo index.css
```css
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap');

:root {
  --color-primary: #4D41C0;
}

* {
    box-sizing: border-box;
    font-family: 'Open Sans', sans-serif;
}

html, body {
    background-color: #E5E5E5;
}

a, a:hover {
  text-decoration: none;
  color: unset;
}
```
- Arquivo index.tsx

```
import 'bootstrap/dist/css/bootstrap.css';
import './index.css';
```

- **COMMIT: Bootstrap**

### Passo: Componente Navbar

ATENÇÃO: no arquivo tsconfig.json: `"baseUrl": "./src"` (reinicie o app)

```js
<header>
    <nav className="container">
        <div className="dsmovie-nav-content">
            <h1>DSMovie</h1>
            <a href="https://github.com/devsuperior" target="_blank" rel="noreferrer">
                <div className="dsmovie-contact-container">
                    <GithubIcon />
                    <p className="dsmovie-contact-link">/devsuperior</p>
                </div>
            </a>
        </div>
    </nav>
</header>
```

```css
header {
    height: 60px;
    background-color: var(--color-primary);
    display: flex;
    align-items: center;
}

.dsmovie-nav-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #fff;
}

.dsmovie-nav-content h1 {
    font-size: 24px;
    margin: 0;
    font-weight: 700;
}

.dsmovie-contact-container {
    display: flex;
    align-items: center;
}

.dsmovie-contact-link {
    margin: 0 0 0 10px;
    font-size: 12px;
}
```

- **COMMIT: Navbar**

### Passo: Rotas

- Instalar React Router DOM
```
yarn add react-router-dom@6.2.1 @types/react-router-dom@5.3.2
```

```js
import {
  BrowserRouter,
  Routes,
  Route
} from "react-router-dom";
import Listing from 'pages/Listing';
import Form from 'pages/Form';
import Navbar from "components/Navbar";

function App() {
  return (
    <BrowserRouter>
      <Navbar />
      <Routes>
        <Route path="/" element={<Listing />} />
        <Route path="/form">
          <Route path=":movieId" element={<Form />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

- **COMMIT: Routes**

### Passo: Tela de formulário

```js
const movie = {
    id: 1,
    image: "https://www.themoviedb.org/t/p/w533_and_h300_bestv2/jBJWaqoSCiARWtfV0GlqHrcdidd.jpg",
    title: "The Witcher",
    count: 2,
    score: 4.5
};
```

```js
<div className="dsmovie-form-container">
    <img className="dsmovie-movie-card-image" src="url" alt="The Witcher" />
    <div className="dsmovie-card-bottom-container">
        <h3>"The Witcher"</h3>
        <form className="dsmovie-form">
            <div className="form-group dsmovie-form-group">
                <label htmlFor="email">Informe seu email</label>
                <input type="email" className="form-control" id="email" />
            </div>
            <div className="form-group dsmovie-form-group">
                <label htmlFor="score">Informe sua avaliação</label>
                <select className="form-control" id="score">
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                    <option>4</option>
                    <option>5</option>
                </select>
            </div>
            <div className="dsmovie-form-btn-container">
                <button type="submit" className="btn btn-primary dsmovie-btn">Salvar</button>
            </div>
        </form >
        <button className="btn btn-primary dsmovie-btn mt-3">Cancelar</button>
    </div >
</div >
```

```css
.dsmovie-form-container {
    max-width: 480px;
    margin: 40px auto;
    padding: 20px;
}

.dsmovie-form {
    width: calc(100% - 20px);
}

.dsmovie-form-group {
    margin-bottom: 20px;
}

.dsmovie-form-group label {
    font-size: 12px;
    color: #aaa;
}

.dsmovie-form-btn-container {
    display: flex;
    justify-content: center;
}

.dsmovie-movie-card-image {
    width: 100%;
    border-radius: 8px 8px 0 0;
}

.dsmovie-card-bottom-container {
    background-color: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 10px 10px 20px 10px;
    border-radius: 0 0 8px 8px;
}

.dsmovie-card-bottom-container h3 {
    color: #4A4A4A;
    text-align: center;
    font-size: 14px;
    font-weight: 700;
    margin-bottom: 10px;
    min-height: 40px;
}

.dsmovie-btn {
    background-color: var(--color-primary);
    font-size: 14px;
    font-weight: 700;
    height: 40px;
    width: 180px;
    display: flex;
    align-items: center;
    justify-content: center;
}
```

