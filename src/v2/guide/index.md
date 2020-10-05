---
title: Introdução
type: guide
order: 2
---

<p class="tip">**Nota da Equipe de Tradução**
Esta tradução é um projeto _open-source_ mantido por um grupo de desenvolvedores, e você também pode colaborar! Caso encontre algum erro na tradução, por favor crie uma _issue_ em [nosso projeto no GitHub](https://github.com/vuejs-br/br.vuejs.org/issues). Sua participação é muito importante!</p>

## O que é Vue.js?

Vue (pronuncia-se /vjuː/, como **view**, em inglês) é um **framework progressivo** para a construção de interfaces de usuário. Ao contrário de outros _frameworks_ monolíticos, Vue foi projetado desde sua concepção para ser adotável incrementalmente. A biblioteca principal é focada exclusivamente na camada visual (_view layer_), sendo fácil adotar e integrar com outras bibliotecas ou projetos existentes. Por outro lado, Vue também é perfeitamente capaz de dar poder a sofisticadas _Single-Page Applications_ quando usado em conjunto com [ferramentas modernas](single-file-components.html) e [bibliotecas de apoio](https://github.com/vuejs/awesome-vue#components--libraries).

Se você gostaria de saber mais sobre Vue antes de mergulhar nele, nós <a id="modal-player"  href="#">criamos um vídeo</a> passeando pelos princípios básicos com um exemplo de projeto.

Se você é um desenvolvedor _frontend_ experiente e quer saber como Vue se compara a outras bibliotecas/_frameworks_, confira a [Comparação com Outros Frameworks](comparison.html).

<div class="vue-mastery"><a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="sponsored noopener" title="Curso Gratuito de Vue.js">Assista a um vídeo-curso gratuito na Vue Mastery</a></div>

## Primeiros Passos

<a class="button" href="installation.html">Instalação</a>

<p class="tip">O guia oficial supõe um nível intermediário em HTML, CSS e JavaScript. Se você é totalmente novo no mundo do _frontend_, mergulhar diretamente em um _framework_ pode não ser a melhor ideia para começar - compreenda primeiro o básico e depois volte! Experiência anterior com outros _frameworks_ ajuda, mas não é obrigatória.</p>

A forma mais simples de testar Vue.js é usando o [exemplo de Olá Mundo no CodeSandbox](https://codesandbox.io/s/github/vuejs/vuejs.org/tree/master/src/v2/examples/vue-20-hello-world). Sinta-se à vontade para abrí-lo em outra aba e acompanhar conosco durante alguns exemplos básicos. Ou, você pode <a href="https://github.com/vuejs/vuejs.org/blob/master/src/v2/examples/vue-20-hello-world/index.html" target="_blank" download="index.html" rel="noopener noreferrer">criar um arquivo <code>index.html</code></a> e incluir Vue com:

``` html
<!-- versão de desenvolvimento, inclui avisos úteis no console  -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

ou:

``` html
<!-- versão de produção, otimizada para tamanho e velocidade -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

No tópico [Instalação](installation.html) se encontram mais opções para instalar o Vue. Nota: **não recomendamos** a iniciantes começar com `vue-cli`, especialmente se você ainda não está familiarizado com ferramentas de _build_ baseadas em Node.js.

Se você preferir algo mais interativo, pode dar uma olhada [nesta série de tutoriais no Scrimba](https://scrimba.com/g/gvuedocs), onde você encontra um misto de _screencast_ e _playground_ de código que pode pausar e executar como quiser.

## Renderização Declarativa

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cQ3QVcr" target="_blank" rel="noopener noreferrer">Tente esta lição no Scrimba</a></div>

No núcleo do Vue.js está um sistema que nos permite declarativamente renderizar dados no DOM (Document Object Model) usando uma sintaxe de _template_ simples:

``` html
<div id="app">
  {{ message }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Olá Vue!'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ message }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Olá Vue!'
  }
})
</script>
{% endraw %}

Acabamos de criar nosso primeiro aplicativo Vue! Isso parece muito similar a renderizar uma _template string_, mas Vue fez bastante trabalho interno. Os dados e o DOM estão agora interligados e tudo se tornou **reativo**. Como podemos ter certeza? Apenas abra o _console_ JavaScript de seu navegador (agora mesmo, nesta página) e atribua um valor diferente em `app.message`. Você verá o exemplo renderizado acima se atualizando de acordo.

Perceba que não temos mais que interagir diretamente com o HTML. Um app Vue acopla-se a um único elemento da DOM (`#app` no nosso caso) e então o controla completamente. O HTML é o nosso ponto de entrada, mas todo o resto acontece dentro da recém criada instância do Vue.

Além de simples interpolação de texto, podemos interligar atributos de elementos:

``` html
<div id="app-2">
  <span v-bind:title="message">
    Pare o mouse sobre mim e veja a dica interligada dinamicamente!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Você carregou esta página em ' + new Date().toLocaleString()
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    Pare o mouse sobre mim e veja a dica interligada dinamicamente!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Você carregou esta página em ' + new Date().toLocaleString()
  }
})
</script>
{% endraw %}

Aqui nos deparamos com algo novo. O atributo `v-bind` que você está vendo é chamado de **diretiva**. Diretivas são prefixadas com `v-` para indicar que são atributos especiais providos pelo Vue, e como você deve ter percebido, aplicam comportamento especial de reatividade ao DOM renderizado. Neste caso, basicamente está sendo dito: "mantenha o atributo `title` do elemento sempre atualizado em relação à propriedade `message` da instância Vue".

Se você abrir seu _console_ JavaScript novamente e informar `app2.message = 'alguma nova mensagem'`, novamente poderá ver que o HTML vinculado - neste caso, o atributo `title` - foi atualizado imediatamente.

## Condicionais e Laços

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQe4SJ" target="_blank" rel="noopener noreferrer">Tente esta lição no Scrimba</a></div>

Também é fácil alternar a presença de um elemento:

``` html
<div id="app-3">
  <p v-if="seen">Agora você me viu</p>
</div>
```
``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="seen">Agora você me viu</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
</script>
{% endraw %}

Vá em frente e informe `app3.seen = false` no _console_. Você verá a mensagem desaparecer.

Este exemplo demonstra que nós podemos interligar dados não apenas ao texto e aos atributos, mas também à **estrutura** do DOM. Mais do que isso, Vue também provê um poderoso sistema de transições que pode automaticamente aplicar [efeitos de transição](transitions.html) quando elementos são inseridos/atualizados/removidos pelo Vue.

Existem mais algumas diretivas, cada uma com sua própria funcionalidade. Por exemplo, a diretiva `v-for` pode ser usada para exibir uma lista de itens usando dados de um Array:

``` html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Aprender JavaScript' },
      { text: 'Aprender Vue' },
      { text: 'Criar algo incrível' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Aprender JavaScript' },
      { text: 'Aprender Vue' },
      { text: 'Criar algo incrível' }
    ]
  }
})
</script>
{% endraw %}

No _console_, informe `app4.todos.push({ text: 'Novo item' })`. Você verá um novo item ser acrescentado dinamicamente à lista.

## Tratando Interação do Usuário

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/czPNaUr" target="_blank" rel="noopener noreferrer">Tente esta lição no Scrimba</a></div>

Para permitir aos usuários interagir com o aplicativo, podemos usar a diretiva `v-on` para anexar escutas a eventos (_event listeners_) que invocam métodos em nossas instâncias Vue:

``` html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Inverter Mensagem</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Olá Vue!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Inverter Mensagem</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Olá Vue!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

Observe que neste método atualizamos o estado da aplicação sem tocar no DOM - todas as manipulações são tratadas pelo Vue, o código que você escreve é focado na lógica de manipulação de dados.

Vue também provê a diretiva `v-model`, que torna a interligação de mão dupla (_two-way binding_) entre a caixa de texto e o estado da aplicação uma moleza:

``` html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Olá Vue!'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Olá Vue!'
  }
})
</script>
{% endraw %}

## Composição com Componentes

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQVkA3" target="_blank" rel="noopener noreferrer">Tente esta lição no Scrimba</a></div>

O sistema de componentes também é outro importante conceito no Vue, por ser uma abstração que proporciona a construção de aplicações de larga escala compostas por pequenos componentes, auto-contidos e frequentemente reutilizáveis. Se nós pensarmos sobre isso, quase qualquer tipo de interface de uma aplicação pode ser abstraída em uma árvore de componentes:

![Árvore de Componentes](/images/components.png)

No Vue, um componente é essencialmente uma instância Vue com opções predefinidas. Registrar um componente no Vue é simples:

``` js
// Define um novo componente chamado todo-item
Vue.component('todo-item', {
  template: '<li>Isso é um item</li>'
})

var app = new Vue(...)
```

Agora você pode compor com isto no _template_ de outro componente:

``` html
<ol>
  <!-- Cria uma instância do componente todo-item -->
  <todo-item></todo-item>
</ol>
```

Mas isto renderizaria o mesmo texto toda vez que um item fosse utilizado, o que não é lá muito interessante. Devemos poder passar os dados do escopo superior (_parent_) para os componentes filhos. Vamos modificar o componente para fazê-lo aceitar uma [prop](components.html#Props):

``` js
Vue.component('todo-item', {
  // O componente todo-item agora aceita uma
  // "prop", que é como um atributo personalizado.
  // Esta propriedade foi chamada de "todo".
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

Agora podemos passar o dado `todo` em cada repetição de componente usando `v-bind`:

``` html
<div id="app-7">
  <ol>
    <!--
      Agora provemos cada todo-item com o objeto todo que ele
      representa, de forma que seu conteúdo possa ser dinâmico.
      Também precisamos prover cada componente com uma "chave",
      a qual será explicada posteriormente.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```
``` js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetais' },
      { id: 1, text: 'Queijo' },
      { id: 2, text: 'Qualquer outra coisa que humanos podem comer' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in groceryList" v-bind:todo="item" v-bind:key="item.id"></todo-item>
  </ol>
</div>
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetais' },
      { id: 1, text: 'Queijo' },
      { id: 2, text: 'Qualquer outra coisa que humanos podem comer' }
    ]
  }
})
</script>
{% endraw %}

Este é um exemplo fictício, mas conseguimos separar nossa aplicação em duas pequenas unidades, sendo que o componente filho está razoavelmente bem desacoplado do componente pai graças à funcionalidade de `props`. Podemos agora melhorar nosso componente `<todo-item>` com _template_ e lógica mais complexos, sem afetar o restante.

Em uma aplicação grande, é essencial dividir todo o aplicativo em componentes para tornar o desenvolvimento gerenciável. Falaremos mais sobre componentes [futuramente neste guia](components.html), mas aqui está um exemplo (imaginário) da aparência que o _template_ de um aplicativo poderia ter com o uso de componentes:

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### Relação com Elementos Customizados

Você pode ter notado que componentes Vue são muito similares aos **Elementos Customizados**, parte da [Especificação de Web Components](https://www.w3.org/wiki/WebComponents/). Isto ocorre pois a sintaxe de componentes Vue foi vagamente modelada a partir da especificação. Por exemplo, implementamos a [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) e o atributo especial `is`. Entretanto, existem algumas diferenças fundamentais:

1. A Especificação de Web Components foi finalizada, mas não está nativamente implementada em todos os navegadores. O Safari 10.1+, Chrome 54+ e Firefox 63+ suportam nativamente os componentes da web. Em comparação, componentes Vue não requerem qualquer tipo de _polyfill_ e funcionam consistentemente em todos os navegadores suportados (IE9 e superiores). Quando necessário, componentes Vue também podem ser envolvidos dentro de um elemento customizado nativo.

2. Componentes Vue oferecem importantes recursos não disponíveis em elementos customizados tradicionais, mais notavelmente: fluxo de dados entre componentes, comunicação com eventos customizados e integração com ferramentas para _build_.

Embora o Vue não use elementos personalizados internamente, ele tem [ótima interoperabilidade](https://custom-elements-everywhere.com/#vue) quando se trata de consumir ou distribuir como elementos personalizados. O Vue CLI também suporta a criação de componentes do Vue que se registram como elementos personalizados nativos.

## Pronto para Mais?

Nós introduzimos brevemente os recursos mais básicos do núcleo do Vue.js - o resto deste guia se aprofundará neles e em outros recursos avançados em um nível muito maior de detalhes, portanto certifique-se de ler tudo!

<div id="video-modal" class="modal"><div class="video-space" style="padding: 56.25% 0 0 0; position: relative;"><iframe src="https://player.vimeo.com/video/247494684?dnt=1" style="height: 100%; left: 0; position: absolute; top: 0; width: 100%; margin: 0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div><script src="https://player.vimeo.com/api/player.js"></script><p class="modal-text">Vídeo por <a href="https://www.vuemastery.com" target="_blank" rel="sponsored noopener" title="Cursos de Vue.js na Vue Mastery">Vue Mastery</a>. Assista ao gratuito <a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="sponsored noopener" title="Cursos de Vue.js na Vue Mastery">Curso de Introdução ao Vue</a>.</div>
