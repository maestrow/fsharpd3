# fsharpd3
Data Driven Documents in F#

Мне нравится библиотека [d3js](https://d3js.org). Нравится то, что она позволяет делать, но не нравится - как это делается. Например, при использовании fluent синтаксиса часто неясно какой тип объекта является результатом очерезного такого вызова. Для того, чтобы обозначать место, где тип объекта меняется, применяют отступы, что некрасиво:

```
  node.append("text")
      .attr("clip-path", function(d) { return "url(#clip-" + d.id + ")"; })
    .selectAll("tspan")
    .data(function(d) { return d.class.split(/(?=[A-Z][^A-Z])/g); })
    .enter().append("tspan")
      .attr("x", 0)
      .attr("y", function(d, i, nodes) { return 13 + (i - nodes.length / 2 - 0.5) * 10; })
      .text(function(d) { return d; });
```

Данный проект - это реализация концепции Data Driven Documents на языке F#. Платформа остается прежней - это JavaScript и браузер, но язык меняется на F#. 

- Для компиляции F# в javascript используется [Fable](http://fable.io/). 
- [fable-elmish](https://github.com/fable-compiler/fable-elmish) - [Elm-like](http://elm-lang.org) abstractions for F# applications targeting Fable. [snabbdom](https://github.com/snabbdom/snabbdom) в качестве виртуальной DOM.

Итак, у нас есть:
- платформа -  браузер
- есть язык - F#, 
- есть библиотека fable-elmish и паттерн elm, позволяющие создавать виджеты, управляемые данными
- есть виртуальная DOM - элементы интерфейса

Остается реализовать удобный API для создания и манипуляции элементыми виртуальной DOM и helper'ы для манипуляции данными, масштабами (scales), а также хелперы для работы с конкретными типами диаграмм/виджетов.
