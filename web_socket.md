# 🌍 Web Socket

------------------------

- [📜 Introdução Web Socket](#-introdução-ao-web--socket)
  - [📚 O que é Web Socket](#-o-que-é-web-socket)
    - [Como funciona](#como-funciona)
    - [⚛️ Exemplo](#-exemplos)
    - [🌲 Biblioteca](#-biblioteca)
    - [🔄 Quando utilizar](#-quando-utilizar)

## 📚 O que é Web Socket

WebSocket é uma tecnologia de comunicação bidirecional que permite a transmissão de dados entre um navegador web e um servidor de maneira eficiente e em tempo real. Diferente do modelo tradicional de requisições HTTP, onde o navegador faz uma solicitação e espera por uma resposta do servidor, com WebSockets, uma conexão persistente é mantida, permitindo a troca de mensagens de ambos os lados a qualquer momento.

### Como Funciona

- Estabelecendo a Conexão: Um WebSocket começa como uma conexão HTTP normal, com um pedido de "upgrade" sendo enviado do cliente para o servidor, solicitando a troca para o protocolo WebSocket. Uma vez aceito, a comunicação é mantida de forma persistente, e mensagens podem fluir em ambas as direções.
- Bidirecionalidade: Uma vez estabelecida a conexão, tanto o cliente quanto o servidor podem enviar mensagens a qualquer momento sem a necessidade de uma solicitação explícita.
- Eventos e Callbacks: A comunicação WebSocket é geralmente baseada em eventos. O cliente e o servidor podem definir manipuladores para eventos como a abertura da conexão, recebimento de uma mensagem, ou fechamento da conexão.


### ⚛️ Exemplo Prático com JavaScript
	```jsx
	
		// Criação de uma nova conexão WebSocket
		const socket = new WebSocket('ws://example.com/socket');
		
		// Evento disparado quando a conexão é aberta
		socket.onopen = () => {
		    console.log('Conexão WebSocket aberta');
		    // Enviando uma mensagem ao servidor
		    socket.send('Olá, servidor!');
		};
		
		// Evento disparado quando uma mensagem é recebida do servidor
		socket.onmessage = (event) => {
		    console.log('Mensagem recebida: ', event.data);
		};
		
		// Evento disparado quando a conexão é fechada
		socket.onclose = () => {
		    console.log('Conexão WebSocket fechada');
		};
		
		// Evento disparado em caso de erro
		socket.onerror = (error) => {
		    console.error('Erro no WebSocket: ', error);
		};
	
	```

### 🌲 Biblioteca

Socket.io é uma biblioteca que facilita a implementação de uma comunicação em tempo real entre o navegador de um usuário e um servidor. Ela é construída sobre a tecnologia de WebSockets e fornece uma interface simples para desenvolver aplicações bidirecionais de maneira eficaz e eficiente.

### 🔄 Quando Utilizar WebSockets?

- Aplicativos de Bate-papo: Permite uma troca rápida de mensagens entre os usuários sem recarregar a página.
- Jogos Online: Proporciona uma experiência fluida, transmitindo dados de jogo em tempo real.
- Plataformas Financeiras: Fornece atualizações em tempo real de preços e cotações, garantindo que os usuários tenham informações atualizadas instantaneamente.
- Atualizações em Tempo Real: Para aplicações que requerem atualizações frequentes, como dashboards de análise ou monitores de sistemas.

