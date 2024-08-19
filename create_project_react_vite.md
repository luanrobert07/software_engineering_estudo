# 🌍 Criando um Projeto com React + Vite

------------------------

- [📜 Introdução ao React + Vite](#-introdução-ao-react--vite)
  - [📚 O que é React e Vite](#-o-que-é-react-e-vite)
    - [Principais Conceitos do React e Vite](#principais-conceitos-do-react-e-vite)
      - [⚛️ Componentes](#-componentes)
      - [🌲 JSX](#-jsx)
      - [🔄 Estado e Props](#-estado-e-props)
      - [🚀 Hooks](#-hooks)
      - [🌐 Router](#-router)
  - [🧠 Objetivo de Aprendizagem](#-objetivo-de-aprendizagem)
  - [✔️ Entrega Mínima](#️-entrega-mínima)

## 📚 O que é [React](https://react.dev) e [Vite](https://vitejs.dev)

React é uma biblioteca JavaScript para a criação de interfaces de usuário. Criada pelo Facebook, é usada para construir aplicativos web rápidos e interativos.

Vite é uma ferramenta de build moderna que proporciona uma experiência de desenvolvimento mais rápida e enxuta para projetos web modernos. É particularmente ótima para projetos que usam frameworks como React.

Pense no React como uma maneira eficiente e sistemática de construir interfaces de usuário, e no Vite como uma ferramenta para agilizar e acelerar o processo de desenvolvimento.

<p align="center">
   <img src="https://vitejs.dev/logo.svg" alt="Vite Logo" width="100" />
   <img src="https://www.patterns.dev/img/reactjs/react-logo@3x.svg" alt="React Logo" width="100" />
</p>

### Principais Conceitos do React e Vite

Vamos explorar os principais conceitos dessas ferramentas. **Não se preocupe se não entender tudo de imediato**. Você ficará mais familiarizado à medida que começar a desenvolver.

#### ⚛️ Componentes

Componentes são os blocos de construção do React. Eles permitem que você divida a interface de usuário em partes reutilizáveis e independentes.

> 📌 Exemplos de componentes podem ser um botão, um formulário ou até uma página inteira.

#### 🌲 [JSX](https://react.dev/docs/introducing-jsx)

JSX é uma extensão de sintaxe para JavaScript, semelhante ao HTML. Com JSX, você pode escrever a estrutura da sua interface de uma maneira clara e familiar.

> 📌 Um exemplo de JSX:
> ```jsx
> const element = <h1>Hello, world!</h1>;
> ```

#### 🔄 Estado e Props

Estado e Propriedades (Props) são conceitos fundamentais para entender como os dados fluem em um aplicativo React.

- **Estado**: Dados que mudam ao longo do tempo e afetam a renderização do componente.
- **Props**: Dados passados para um componente, semelhantes aos parâmetros de uma função.

> 📌 Um exemplo simples de uso de estado e props:
> ```jsx
> function Welcome(props) {
>   return <h1>Hello, {props.name}</h1>;
> }
>
> class Clock extends React.Component {
>   constructor(props) {
>     super(props);
>     this.state = {date: new Date()};
>   }
>
>   render() {
>     return (
>       <div>
>         <h1>It is {this.state.date.toLocaleTimeString()}.</h1>;
>       </div>
>     );
>   }
> }
> ```

#### 🚀 [Hooks](https://react.dev/docs/hooks-intro)

Hooks são uma adição recente ao React que permitem o uso de estado e outras funcionalidades de React sem escrever uma classe.

> 📌 Exemplo de uso de um Hook:
> ```jsx
> import { useState } from 'react';
>
> function Example() {
>   const [count, setCount] = useState(0);
>
>   return (
>     <div>
>       <p>You clicked {count} times</p>
>       <button onClick={() => setCount(count + 1)}>
>         Click me
>       </button>
>     </div>
>   );
> }
> ```

#### 🌐 [Router](https://reactrouter.com/)

React Router é uma biblioteca para roteamento no React, permitindo a criação de navegação de página única (SPA).

> 📌 Exemplo de configuração de rotas:
> ```jsx
> import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
>
> function App() {
>   return (
>     <Router>
>       <Switch>
>         <Route path="/about">
>           <About />
>         </Route>
>         <Route path="/users">
>           <Users />
>         </Route>
>         <Route path="/">
>           <Home />
>         </Route>
>       </Switch>
>     </Router>
>   );
> }
> ```

## 🧠 Objetivo de Aprendizagem

O objetivo é aprender como criar um projeto React usando Vite, entendendo a configuração e os conceitos básicos para começar a desenvolver uma aplicação web moderna.

## ✔️ Entrega Mínima

1. **Inicialização do Projeto**: Inicializar um novo projeto React usando Vite.
2. **Componentes Básicos**: Criar alguns componentes básicos para exibir uma interface de usuário simples.
3. **Gerenciamento de Estado**: Implementar gerenciamento de estado usando hooks.
4. **Roteamento**: Configurar roteamento para navegar entre diferentes componentes/páginas.

### Inicialização do Projeto com Vite

1. **Criar um novo projeto Vite:**
   ```bash
   npm create vite@latest my-react-app -- --template react
   cd my-react-app
   npm install
   npm run dev
   ```

2. **Estrutura de Pastas:**
	```bash
		my-react-app/
	├── public/
	├── src/
	│   ├── assets/
	│   ├── components/
	│   ├── App.jsx
	│   ├── main.jsx
	├── index.html
	├── package.json
	```
	
3. **Exemplo de Componente Básico:**
	```bash
		// src/components/Welcome.jsx
	export default function Welcome({ name }) {
	  return <h1>Olá, {name}!</h1>;
	}
	```

4.**Usando o Componente:**
	```bash
		// src/App.jsx
	import Welcome from './components/Welcome';
	
	function App() {
	  return (
	    <div>
	      <Welcome name="Mundo" />
	    </div>
	  );
	}
	
	export default App;
	```
	

	