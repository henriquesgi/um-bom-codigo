
  

## Por que escrever um bom código?
Este artigo contém sugestões para melhorar a legibilidade, manutenção e entendimento do seu código.  

Um código é bem semelhante a um livro.  
Da mesma forma que um livro é escrito para que outras pessoas o leiam, um código também é.  
Um livro de linguagem simples proporcionará interesse e fácil entendimento, já um livro complexo e de linguagem complicada resultará em uma leitura cansativa, tediosa e obrigará o leitor a repetir um mesmo trecho diversas vezes.  
Sempre escreva um código pensando em seus leitores, em outras palavras, **crie códigos de tal maneira que alguém leigo consiga ter uma certa ideia do que o código faz.**

Recomendo que você leia algum Clean Code, e de preferência para a linguagem de programação que você mais se identifica, no meu caso o [JavaScript Clean Code](https://github.com/ryanmcdermott/clean-code-javascript) ou o [TypeScript Clean Code](https://github.com/labs42io/clean-code-typescript), recomendo também que conheça os princípios [SOLID](https://en.wikipedia.org/wiki/SOLID) assim como os [Design Patterns](https://en.wikipedia.org/wiki/Software_design_pattern).

Existem processos que visam assegurar a qualidade, como o [Code Review](https://en.wikipedia.org/wiki/Code_review), e é de grande importância o seu uso, afinal, tais processos têm como objetivo manter os padrões estipulados e amenizar problemas que podem passar despercebidos durante o desenvolvimento.  

### O que você deve saber antes de começar a programar?
Estude inglês, isso é imprescindível.  
Aprenda a pesquisar.  
Um desenvolvedor irá estudar desde o momento em que escolheu a sua profissão até o final de sua vida, acostume-se com essa rotina.

### Qual idioma usar?
O recomendado é criar códigos em inglês, porém, caso o seu produto tenha muitos termos que sem tradução ou sem uma tradução adequada, prefira criar um código inteiramente em português.  
**JAMAIS UTILIZE DOIS IDIOMAS NO CÓDIGO**, isso irá dificultar o entendimento do seu código e confundir os leitores.  

É óbvio que você não será capaz de traduzir métodos, funções, classes e termos específicos de uma linguagem de programação ou de bibliotecas de terceiros, logo, ao optar pelo português em seu código, é interessante manter em português tudo criado por você, ou seja, mantenha em português as regras de negócio, utilitários, classes, métodos, variáveis e entidades, por exemplo.

Não existe um modelo de código perfeito, livre de dúvidas ou sem discussões.  
Sempre existirão discussões envolvendo pequenos detalhes não abordados em praticamente nenhum guia.  

```JavaScript
// Código usando o português
var user                        // ruim
var usuario                     // bom

function calculateArea() {...}  // ruim
function calcularArea() {...}   // bom

var collectionUsuario = [...]   // ruim
var colecaoUsuario = [...]      // bom
var usuarios = [...]            // essa é a melhor escolha, um nome no plural indica que você pode ter mais de um usuário
```

### Escolha uma convenção para nomes
Escolha uma convenção para nomes [Naming convention](https://en.wikipedia.org/wiki/Naming_convention_(programming)) e respeite essa decisão.  

```JavaScript
// Usando o lower camel case:
var nomemenino = 'Pedro'  // ruim
var nome_menino = 'Pedro' // ruim
var nomeMenino = 'Pedro'  // bom

var IDUsuario = 001       // ruim
var ID_usuario = 001      // ruim
var IdUsuario = 001       // bom
// Não interessa se a palavra é uma abreviação de algo ou tem duas letras maiúsculas, como ID, respeite o padrão escolhido
```

Conforme já mencionado, não existe uma regra ou padrão que se encaixará perfeitamente em todos os cenários, por exemplo:

```JavaScript
// Imagine uma função que receba um usuario como parâmetro e necessite de uma variável com o nome usuário
// Nesse caso, pode ser utilizado algo como "_usuario", desrespeitando a convenção de nomes
function atualizarUsuario(usuario) {
  var _usuario = db.usuarios.update({
    { id: usuario.id },
    { $set: { nome: usuario.nome } },
  })
}
```
> Alguns desenvolvedores JS consideram que variáveis iniciadas com "_" como uma forma de identificar que a variável é "privada" ao escopo, ou seja, consideram que são variáveis privadas à função, classe, bloco de código...  
Saiba que é apenas uma sugestão, não é nada oficial ou definido pelo ECMAScript.  

O seguintes tópicos são bem parecidos que os que são encontrados em guias de Clean Code.  
Optei por os escrever devido a sua grande importância, eles são fundamentais para o entendimento do código.  

### Variáveis
Nomeie variáveis de acordo com o que elas armazenam.  
Não use abreviações.  
Ao criar uma variável tenha em mente "o que essa variável armazena?".  
Não use números mágicos.  

```JavaScript
var valores = { nome: 'Rodrigo' } // ruim
var pessoa = { nome: 'Rodrigo' }  // bom

var n = 'Silvio'                  // ruim
var nome = 'Silvio'               // bom

if (velocidadeMedida > 60) {...}  // ruim
// O que significa 60?

const velocidadePermitida = 60    // bom
if (velocidadeMedida > velocidadePermitida) {...}
```

### Vetores
É recomendado que um vetor seja uma coleção de apenas um determinado tipo de dado

```JavaScript
var dados = ['laranja', 49, 'soldado', { nome: 'joão' }]    // ruim
dados.forEach((dado) => {
  // Os dados terão mais de um comportamento, como você vai tratar isso?
  // Será necessário um tratamento diferente para cada dado
})

var frutas = ['limão', 'laranja', 'melancia']                // bom
frutas.forEach((fruta) => {
  // A correta abstração permite um tratamento adequado juntamente com um único comportamento
  // A correta nomemclatura do vetor e do elemento de iteração criam um código de boa legibilidade
})
```

### Funções
Uma função deve ser capaz de realizar apenas uma ação;
O nome de uma função deve indicar o que ela faz;
Se você for escrever o seu código em português, uma boa sugestão para nomear funções é utilizar verbos no infinitivo;
Se a função faz mais de uma ação ela está errada;
Quando uma função espera receber X, o seu parâmetro deve-se chamar X e não algo aleatório.
```
Exemplos:
function calculoArea() { ... }		// ruim
function calculandoArea() { ... }	// ruim
function calcularArea() { ... }		// bom

// ruim
function calcularArea(base, altura) {
	var area = base * altura

	// A função não calcula apenas a área, ela tem outras responsabilidades
	if(area > 100) {
		return 'Essa figura está além do limite'
	}
	return area
}

// bom
function calcularArea(base, altura) {
	return base * altura
}
// A função não deve fazer nada além do que ela é destinada a fazer

// ruim
function buscarUsuario(data) {
	const usuario = db.usuarios.get(data)
}

// bom
function buscarUsuario(id) {
	// A busca será feita por ID, logo, espera-se um ID como parâmetro e isso deve ser claro
	const usuario = db.usuarios.get(id)
}








" ou ' dentro de templatestrings

espaços depois de blocos de código

leia o código e entenda

pesquise antes de ir de acordo com sua intuição
