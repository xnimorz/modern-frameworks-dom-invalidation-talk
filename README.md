## Материал доклада "Работа с DOM в JS фреймворках"

Ссылка на слайды презентации: https://slides.com/nikmostovoy/deck-2bae97/

Также копия есть в html варианте в репозитории — https://github.com/xnimorz/modern-frameworks-dom-invalidation-talk/raw/master/HolyJs-slides-RU.html (но нужно руками загружать)

### Полный пример кода invalidator + updater + inverseInvalidator

```js
import React, { useState } from "react";
import Component from "./Component";

function App() {
  const [ articles, setArticles ] = useState([
    { id: 1, text: "foo" },
    { id: 2, text: "bar" },
    { id: 2, data: {} },
  ]);   
  const [ title, setTitle ] = useState('Hello world');

  const updater = {
	h1: {
      update: (ctx, $1) => {ctx.el.textContent = $1}
    },
    Content: {
      update: () => {},
    }
  }
  
  const invalidator = {
    div: {
      children: {
        h1: {deps: [title]},
        Content: {deps: [title ? title : 'stub', articles]},
      },
      deps: [],
    } 
  }
  
  const invertedInvalidator = {
    title: [h1, Content],
    articles: [Content],
  }
   
  return (
    <div>
      <h1>{title}</h1>
      <Content title={title ? title : 'stub'} articles={articles} />
    </div>
  );
}
```

### Полезные ссылки

https://mohebifar.github.io/vidact/ — vidact

https://rawgit.com/krausest/js-framework-benchmark/master/webdriver-ts-results/table.html — сравнение фронтенд-библиотек

https://astexplorer.net/ — ast explorer

https://svelte.dev/repl/668a0c17c30540e29a2c017b203a8ab0?version=3.23.2 — REPL с примером на svelte