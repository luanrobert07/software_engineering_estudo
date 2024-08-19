# 🌍 React

------------------------

- [📜 Introdução ao React](#-introdução-ao-react)
  - [📚 O que é React](#-o-que-é-react)
    - [Principais conceitos do React](#principais-conceitos-do-react)
      - [⚛️ Componentes](#-componentes)
      - [🌲 JSX](#-jsx)
      - [🔄 Estado e Props](#-estado-e-props)
      - [🚀 Hooks](#-hooks)
      - [🌐 Router](#-router)
  - [🧠 Objetivo de aprendizagem](#-objetivo-de-aprendizagem)
  - [✔️ Entrega mínima](#️-entrega-mínima)

# 📚 Introdução ao Clean Code

O Clean Code nasceu em um cenário de transformação digital. Neste cenário, um dos maiores desafios para desenvolvedores é escrever códigos simples de ler, funcionais e que atendam as expectativas dos clientes. Para obter esse resultado, é imprescindível seguir as boas práticas da arquitetura de software. 

O Clean Code é uma abordagem que permite às equipes entregar sistemas operantes, intuitivos e facilmente escaláveis. Ele entende que mesmo um código ruim pode funcionar, mas que é preciso mais que isso para suprir as necessidades do contratante de forma adequada, evitando bugs e falhas. 

## O que é?
Escrever código-fonte de maneira clara, legível e organizada. Seu objetivo é tornar sua compreensão, manutenção e colaboração por parte de outros desenvolvedores posteriores mais simples e fácil. 

### Princípios
- Nomenclatura Clara e Significativa
A escolha dos nomes para variáveis e funções deve ser feita com cuidado. Um bom nome explica claramente o propósito da variável ou função, facilitando a compreensão do código. Evite abreviações obscuras e seja descritivo. Por exemplo, use totalHoursInAYear em vez de simplesmente h.

```Jsx

	//abreviação obscura
	const h = 8760
	for (i=0;  i < h; i++) {
		
	}
	//forma descritiva
	const totalHoursInAYear = 8760
	for (i=0;  i < totalHoursInYear; i++) {
		
	}
	
```

- Evite Números Mágicos
Números mágicos são valores numéricos com significado não claro no código. Substitua-os por constantes nomeadas para tornar o código mais legível. Por exemplo, substitua 86400 (número de segundos em um dia) por SEGUNDOS_POR_DIA.

- Reduza Comentários Desnecessários
Comentários devem ser usados para documentar o código, não para explicar o que uma variável ou função faz. Um código bem escrito deve ser autoexplicativo. Se sentir necessidade de adicionar um comentário para explicar o que uma linha de código faz, considere refatorar essa linha para torná-la mais clara.

- Funções Curtas e Focadas
Cada função deve ter um único propósito e executá-lo bem. Evite funções longas e complexas, dividindo-as em funções menores se necessário. Isso não apenas torna o código mais limpo, mas também facilita o teste e a manutenção.

Um código sem aplicação dessa estratégia:

async function notifyUsers(userIds, message) {
    for (const userId of userIds) {
        const user = await User.findByPk(userId);
        if (user && user.isSubscribed) {
            await Notifications.create({
                date: new Date(),
                user_id: userId,
                message,
                emailNotify: true
            });
        } else {
            await Notifications.create({
                date: new Date(),
                user_id: userId,
                message,
                emailNotify: false
            });
        }
    }
}
Um código com aplicação dessa estratégia:

const createNotification = async (user, message) => {
    await Notifications.create({
        date: new Date(),
        user_id: user.id,
        message,
        emailNotify: user.isSubscribed
    });
};

async function notifyUsers(userIds, message) {
    for (const userId of userIds) {
        const user = await User.findByPk(userId);
        if (user) {
            await createNotification(user, message);
        }
    }
}
No primeiro código, a lógica para criar uma notificação estava sendo repetida em dois lugares dentro da mesma função. E com a refatoração usando essa estratégia conseguimos eliminar essa repetição, assim o princípio DRY (Don't Repeat Yourself) é aplicado, que é uma prática fundamental no desenvolvimento de software para reduzir a duplicação e facilitar futuras alterações.

- Encapsule Condições
Encapsular condições complexas em variáveis ou funções torna o código mais legível. Em vez de ter uma longa expressão condicional, use uma variável com um nome descritivo que explique o propósito da condição.

//Forma não encapsulada
const getUSTime = time => {
	if(time =< 12) {
		return time + "AM"
	} else {
		return time + "PM"
	}
}
//Forma encapsulada
const getUSTime = time => {
	const timeIsEqualsOrBellowTwelve = time =< 12
	if(timeIsEqualsOrBellowTwelve) {
		return time + "AM"
	} 
	return time + "PM"
}

- Evite Estruturas de Controle Complexas
Prefira estruturas de controle simples e evite aninhamentos profundos. Use retornos antecipados para reduzir a complexidade e melhorar a legibilidade.

### ⚛️ Exemplos para iniciar sua prática

Mistura de idiomas.
Como mencionado anteriormente, é ideal seguir um padrão dentro do nosso código, inclusive para o idioma escrito. Entre os padrões que podemos citar,  um deles é o inglês tanto para a escrita de código quanto para documentações. Normalmente as linguagens possuem como padrão comandos e palavras-chave em inglês.

Evitar:

let moeda = {
	value: 10,
	country: 'USA'
} 
Fazer:

let currency = {
	amount: 10,
	country: 'USA'
} 
Dê nomes significativos e dentro do contexto aplicado evitando a abreviação.
Evitar:

const fName = 'Sheldon Lee Cooper'
Fazer:

const fullName = 'Sheldon Lee Cooper'
Evite nomes redundantes

Evitar:

let person = {
	personName: 'Sheldon',
	personLastName: 'Lee Cooper',
	personAge: 42,
}
Fazer:

let person = {
	name: 'Sheldon',
	lastName: 'Lee Cooper',
	age: 42,
}
Evite colocar tipos no nome da variável
Evitar:

let arrayOfFruits = [ 'banana', 'morango', 'manga' ]
Fazer:

let fruits = [ 'banana', 'morango', 'manga' ]
Utilize um padrão para escrever e crie constantes para os números mágicos.

Evitar:

function calcMedia (a, b) {
	const media_notes = (a + b) / 2

	if (media_notes >= 6) {
		return 'Media alcançada'
	}
	return 'Media não alcançada'
}
Fazer:

function calculateAverage (noteA, noteB) {
	const minValue = 6
	const success = 'Media alcançada'
	const noSuccess = 'Media não alcançada'
	const average = (noteA + noteB) / 2

	return (average >= minValue) ? success : noSuccess
}
Evite encher seu código de comentários que não sejam relevantes
Utilize os comentários a seu favor, como, por exemplo, para explicar regras de negócio, decisões e motivações que foram escolhidas para o contexto que determinada funcionalidade foi escrita.

Evitar:

 /*
	função que entra em contato com a API de conversões 
	de moeda.
	@params
	valor da moeda, pais
	@return
	valor da moeda convertido
*/
function currencyCoin(coin, country) {...}
Tente escrever funções menores, delegando a elas apenas uma tarefa, assim o código fica mais claro durante a leitura.
Evitar:

Neste primeiro exemplo é feita a separação de números pares e impares, assim como suas somas e multiplicações, o que pode tornar mais dificil a compreensão

function splitArrayNumbers (list) {
	let pairs = []
	let odd = []
	let pairSum = 0
	let oddMultiplication = 1
	
	for (let item of list) {
		if (num % 2 === 0) {
			pairs.push(num)
			pairSum += num
		} else {
			odd.push(num)
			oddMultiplication *= num
		}
	}
	
	return {
		pairs,
		odd,
		pairSum,
		oddMultiplication
	}
}
Fazer:

Para melhorar, podemos fazer um ajuste simples, separando em funções especificas para cada funcionalidade

function splitNumbers (list) {
	let pairs = []
	let odd = []
	
	for (let item of list) {
		if (item % 2 === 0) {
			pairs.push(item)
		} else {
			odd.push(item)
		}
	}
	
	return { pairs, odd }
}

function calculate (list) {
	let pairSum = 0
	let oddMultiplication = 1
	
	for (let item of list) {
		if (item % 2 === 0) {
			pairSum += item
		} else {
			oddMultiplication *= item
		}
	}
	
	return { pairSum, oddMultiplication }
}
Evite inserir parâmetros demais nas funções
Uma função idealmente deve receber no máximo 2 parâmetros, caso seja necessário passar mais, o ideal é fazer então com que essa função receba um objeto ou array como parâmetro, dependendo da funcionalidade.

Evitar

function calculateAverage ( note1, note2, note3, note4) {
	let average = (note1 + note2 + note3 + note4 ) / 4
	return average
}

const name = “Jhony Test”
const average = calculateAverage (8,10,6,4)

console.log(`A média do aluno ${name} é ${average}.`)
Fazer:

function calculateAverage ( notes) {
	let sum = 0
	for (let note of notes) {
		sum += note
	}
	
	let average = sum / notes.length
	return average
}

const name = “Jhony Test”
const notes = [8, 10, 6, 4]
const average = calculateAverage (notes)

console.log(`A média do aluno ${name} é ${average}.`)
Priorize passar valores padrão
Quando se está escrevendo uma função, tente priorizar a prática de passar valores padrão, isso evita que o código quebre caso algum dado esteja com o valor errado.

Neste exemplo, caso um dos valores não seja passado para a função, poderá ocorrer erros durante a execução:

function calculateTotalPrice (value, quantity, rate) {
	const priceWithoutRate = value * quantity
	const priceWithRate = priceWithoutRate + (priceWithoutRate * rate)
	return priceWithRate
}

Atribuindo valores padrão, mesmo que um dos parâmetros não seja passado, a função irá calcular com os valores padrões:

function calculateTotalPrice (value, quantity = 1, rate = 0.1) {
	const priceWithoutRate = value * quantity
	const priceWithRate = priceWithoutRate + (priceWithoutRate * rate)
	return priceWithRate
}

calculateTotalPrice(100); // Saída: 110
calculateTotalPrice(50, 2); // Saída: 110
calculateTotalPrice(50, 2, 0.2); // Saída: 120
Assim como ter um padrão para escrever as variáveis as funções se encaixam neste item, então padronize a escrita e as nomenclaturas de funções.

Evitar:

getuserData()
getProductRecord()
get_email_info()
Fazer:

getUserData()
getProductData()
getEmailInfoData()