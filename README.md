

Vamos começar a análise com um `form` bem simples:

```html
  <form action="api/beers">
    <label>
      <span>
        Name:
      </span>
      <input type="text" data-ng-model="beer.name" />
    </label>
    <label>
      <span>
        Price:
      </span>
      <input type="number" min="0" data-ng-model="beer.price" />
    </label>
    <label>
      <span>
        Alcohol %:
      </span>
      <input type="number" data-ng-model="beer.alcohol" />
    </label>
    <label>
      <span>
        Description
      </span>
      <textarea name="" data-ng-model="beer.description"></textarea>
    </label>
    <div class="form-buttons-wrapper">
      <button data-ng-click="save(beer)">Save</button>
      <button>Reset</button>
    </div>
  </form>
```

Vamos iniciar criando módulo de Beers no Angular, para isso crie uma pasta chamada `beers` dentro de uma pasta chamada `modules`, antes de iniciarmos o módulo de Beer, vamos criar o `app.js` que é o arquivo central desse projeto com Angular.

```js
(function() {

  'use strict';

  // Declare app level module which depends on views, and components
  angular.module('myApp', [
    'ngRoute',
    'myApp.Beers'
  ]).
  config(['$routeProvider', function($routeProvider) {
    $routeProvider.otherwise({redirectTo: '/beers'});
  }]);

})();

```

Agora vamos criar o módulo `myApp.Beers` com a definição do módulo e suas dependências, dentro de `modules/beers` crie o arquivo index.js:

```js
(function() {
  'use strict';

  angular.module('myApp.Beers', ['ngRoute'])
  .config(['$routeProvider', function($routeProvider) {
    $routeProvider.when('/beers/create', {
      templateUrl: 'modules/beers/views/form.html',
      controller: 'BeersCreateCtrl'
    });
  }])

})();
```

Começamos fazendo a definição da rota que vai mostrar o form que criamos inicialmente, salve esse HTML como `form.html` em `modules/beers/viewsform.html`, como é uma partial só precisamos do que interessa:

```html
<h2>Cadastro de Cerveja</h2>
<form action="api/beers">
  <label>
    <span>
      Name:
    </span>
    <input type="text" data-ng-model="beer.name" />
  </label>
  <label>
    <span>
      Price:
    </span>
    <input type="number" min="0" data-ng-model="beer.price" />
  </label>
  <label>
    <span>
      Alcohol %:
    </span>
    <input type="number" data-ng-model="beer.alcohol" />
  </label>
  <label>
    <span>
      Description
    </span>
    <textarea name="" data-ng-model="beer.description"></textarea>
  </label>
  <div class="form-buttons-wrapper">
    <button data-ng-click="save(beer)">Save</button>
    <button>Reset</button>
  </div>
</form>
```

Agora crie um arquivo chamado `controllers.js` dentro de `modules/beers/`, onde colocaremos a definição do nosso *Controller* para criar uma Cerveja já fazendo a chamada para seu *Service*.


