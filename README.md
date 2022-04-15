## Por que escrever um bom código?
Um código é bem semelhante a um livro.  
Da mesma forma que um livro é escrito para que outras pessoas o leiam, um código também é.  
Um livro de linguagem simples proporcionará interesse e fácil entendimento, já um livro complexo e de linguagem complicada resultará em uma leitura cansativa, tediosa e obrigará o leitor a repetir um mesmo trecho diversas vezes.  
Sempre escreva um código pensando em seus leitores, em outras palavras, **crie códigos de tal maneira que alguém leigo consiga ter uma certa ideia do que o código faz.**

Recomendo que você leia algum Clean Code, e de preferência para a linguagem de programação que você mais se identifica, no meu caso o [JavaScript Clean Code](https://github.com/ryanmcdermott/clean-code-javascript) ou o [TypeScript Clean Code](https://github.com/labs42io/clean-code-typescript), recomendo também que conheça os princípios [SOLID](https://en.wikipedia.org/wiki/SOLID) assim como os [Design Patterns](https://en.wikipedia.org/wiki/Software_design_pattern).

Busque utilizar ferramentas como o [ESLint](https://eslint.org/) e o [Prettier](https://prettier.io/) para verificar problemas e manter padrões de formatação do código.

Acompanhar novidades, atualizações e artigos como [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices) é essencial para melhorar o nível dos seus códigos. Quanto mais conhecimento, melhor.  

Saiba também que existem processos que visam assegurar a qualidade, como o [Code Review](https://en.wikipedia.org/wiki/Code_review), e é de grande importância o seu uso, afinal, tais processos têm como objetivo manter os padrões estipulados e amenizar problemas que podem passar despercebidos durante o desenvolvimento.  

### Qual idioma usar?
O recomendado é criar códigos em inglês, porém, caso o seu produto tenha muitos termos sem tradução, sem uma tradução adequada ou até mesmo se a sua equipe não tem um nível de inglês satisfatório, prefira criar um código inteiramente em português.  
**EVITE MISTURAR IDIOMAS NO CÓDIGO**, isso irá dificultar o entendimento e causar confusões.  

É óbvio que você não será capaz de traduzir métodos, funções, classes e termos específicos de uma linguagem de programação ou de bibliotecas de terceiros, logo, ao optar pelo português em seu código, é interessante manter em português tudo criado por você, ou seja, mantenha em português as regras de negócio, utilitários, entidades, classes, métodos, variáveis, por exemplo.

Não existe um modelo de código perfeito, livre de dúvidas ou sem discussões, sempre existirão dúvidas envolvendo pequenos detalhes não abordados em praticamente nenhum guia.  

```JavaScript
// Código usando o português
const user                        	// ruim
const usuario                    	// bom

function calculateArea() {...}		// ruim
function calcularArea() {...}   	// bom

const collectionUsuario = [...]   	// ruim
const colecaoUsuario = [...]     	 // bom
```

### Escolha uma convenção para nomes
Escolha uma [Naming convention](https://en.wikipedia.org/wiki/Naming_convention_(programming)) e respeite essa decisão.  

```JavaScript
// Usando o lower camel case:
const nomemenino = 'Pedro'  // ruim
const nome_menino = 'Pedro' // ruim
const NomeMenino = 'Pedro'  // ruim
const nomeMenino = 'Pedro'  // bom

const IDUsuario = 001       // ruim
const ID_usuario = 001      // ruim
const IdUsuario = 001       // ruim
const idUsuario = 001       // bom
// Não interessa se a palavra é uma abreviação ou algo como ID, respeite o padrão escolhido
```

Conforme já mencionado, não existe uma regra ou padrão que se encaixe perfeitamente em todos os cenários:

```JavaScript
// Imagine uma função que receba um usuario como parâmetro e necessite de uma variável com o nome usuário
// Nesse caso, pode ser utilizado algo como "_usuario", desrespeitando a convenção de nomes
function atualizarUsuario(usuario) {
  const _usuario = db.usuarios.update({
    { id: usuario.id },
    { $set: { nome: usuario.nome } },
  })
}
```

> Alguns desenvolvedores JS consideram que variáveis iniciadas com "_" como uma forma de identificar que a variável é "privada" ao escopo, ou seja, consideram que são variáveis privadas à função, classe, bloco de código...  
> Saiba que é apenas uma sugestão, não é nada oficial ou definido pelo ECMAScript.  

Os seguintes tópicos são bem parecidos com o que é descrito em guias de Clean Code.  
Optei por escrever apenas para exemplificar um pouco esse guia, demonstrando a importância do que foi descrito, no caso, o Clean Code:  

### Variáveis
Nomeie variáveis de acordo com o que elas armazenam.  
Não use abreviações.  
Ao criar uma variável tenha em mente "o que essa variável armazena?".  
Não use números mágicos.  

```JavaScript
const valores = { nome: 'Rodrigo' }	// ruim
const pessoa = { nome: 'Rodrigo' } 	// bom

const n = 'Silvio'                  	// ruim
const nome = 'Silvio'               	// bom

if (velocidadeMedida > 60) {...}	// ruim
					// O que significa 60?

const velocidadePermitida = 60    	// bom
if (velocidadeMedida > velocidadePermitida) {...}
```

### Vetores
É recomendado que um vetor seja uma coleção de apenas um determinado tipo de dado.

```JavaScript
var dados = ['laranja', 49, 'soldado', { nome: 'joão' }]    // ruim
dados.forEach((dado) => {
  // Os dados terão mais de um comportamento, como você vai tratar isso?
  // Será necessário um tratamento diferente para cada dado
})

var frutas = ['limão', 'laranja', 'melancia']                // bom
frutas.forEach((fruta) => {
  // A correta abstração permite um tratamento adequado juntamente com um único comportamento
  // A correta nomenclatura do vetor e do ponteiro criam um código de boa legibilidade
})
```

### Funções
Uma função deve ser capaz de realizar apenas uma ação, e isso é extremamente importante.  
O nome de uma função deve indicar o que ela faz.  
Ao escrever o seu código em português, uma boa sugestão para nomear funções é utilizar verbos no infinitivo, indicando que uma ação será feita.  
Quando uma função espera receber X, o seu parâmetro deve-se chamar X e não algo aleatório e sem relação.  

```JavaScript
function calculoArea() {...}		// ruim
function calculandoArea() {...}		// ruim
function calcularArea() {...}		// bom

// A função não calcula apenas a área, ela tem outras responsabilidades
function calcularArea(base, altura) {
	const area = base * altura	
	
	if (area > 100) {
		return 'Erro!'
	}
	return area
}

// Agora repare que são utilizadas duas funções com responsabilidades únicas
// "validarTamanhoArea" sabe apenas o que ela deve fazer e nada além disso
function calcularArea(base, altura) {
	return base * altura
}

function validarTamanhoArea(area, limite = process.env.limite) {
	if (area > limite) {
		return 'Erro!'
	}
	return area
}

function buscarUsuario(data) {			// ruim
	const usuario = db.usuarios.get(data)	// O que "data" representa na entidade de usuários?
}

function buscarUsuario(id) {			// bom
	const usuario = db.usuarios.get(id)	// Sabe-se que a busca será feita pela chave única
}
```

### Excesso de funções
Responda a seguinte pergunta antes de ir para a próxima linha: Você sabe o que é uma função?  
Considerando o contexto desse artigo e de acordo com a [Wikipedia](https://en.wikipedia.org/wiki/Subroutine), uma função tem como principais objetivos: criar subrotinas para reduzir complexidade, reduzir códigos que seriam duplicados, dividir um programa em "etapas" de execução, melhorar a legibilidade do código...  
Mas por que mostrar o óbvio?  
Porque existem programadores que utilizam funções em absolutamente todo o código, fazendo com que o leitor fique "pulando" linhas a todo instante.

```JavaScript
function retornarData() {
	return new Date()
}

const informacoesFuncionario = {
	nome: 'João',
	// Por não ser uma biblioteca de terceiro é provável que o leitor pare e analize o que a função faz
	hora: retornarData()
}

fecharPonto(informacoesFuncionario)
```

A função acima não recebe parâmetros e também não realiza operações, será que ela é útil?

Repare que no seguinte exemplo a leitura é sem interrupções e não causa a perda de foco do leitor:

```JavaScript
const informacoesFuncionario = {
	nome: 'João',
	hora: new Date()
}

fecharPonto(informacoesFuncionario)
```

Use funções de forma sábia, sempre faça com que elas melhorem o código.
