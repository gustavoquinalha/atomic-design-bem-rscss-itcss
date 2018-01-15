![Image](http://atomicdesign.bradfrost.com/images/content/instagram-atomic.png)

# Atomic Design + BEM + RSCSS

## Composição

- Átomo (Items do styleguide/Variáveis)
- Molécula (Styleguide)
- Organismo (Micro-componentes)
- Template (Componente)
- Pages (Pàgina)

## Estrutura HTML
- Flexbox
- Container é responsável pelo comportamento dos items
- Baseado em container e item ou pai e filho
EX:

```html
<div class="container">
  <div class="item"></div>
</div>

<div class="pai">
  <div class="filho pai">
    <div class="filho"></div>
  </div>
  <div class="filho"></div>
  <div class="filho"></div>
</div>
```

## Nomenclatura das classes
> Based in BEM | http://getbem.com/naming/
- Block
- Element
- Modifier

```scss
block--element-modifier

<div class="block">
	<div class="block__element block__element-red">
    <div class="block__element--image">...</div>
    <div class="block__element--text">...</div>
    <div class="block__element--button">...</div>
  </div>
</div>
  
<button class="button">Normal button</button>
<button class="button button--state-success">Success button</button>
<button class="button button--state-danger">Danger button</button>
```

## Estrutura de pastas

- assets
  - css
    - main.scss
    - base
      - _variables.scss
      - _reset.scss
    - styleguide
      - _grid.scss
      - _template.scss
      - _colors.scss
      - _borders.scss
      - _fonts.scss
      - _forms.scss
      - _buttons.scss
      - _icons.scss
    - components
      - _menu.scss
      - _footer.scss
      - _search.scss
      - _title.scss
      - _price-tables.scss
      - cards/
        - _card.scss
        - _simple-card.scss
  - images
  - js
- pages
  - home/
    - index.html
  - contact/
    - index.html
  - prices/
    - index.html
  - login/
    - index.html
- components
  - menu/
    - index.html
  - footer/
    - index.html
  - search/
    - index.html
  - title/
    - index.html
  - price-tables/
    - index.html
  - cards/
    - index.html
- index.html

### Button example
_variables.scss
```scss
// colors
$white: #fff;
$black: #000;
$color-primary: #0081ff;
$color-secundary: #ff4455;
$grey: #ddd;
```

_buttons.scss
```scss
$btn-size-small: 22px;
$btn-size: 32px;
$btn-size-large: 42px;
$btn-radius: 4px;
$btn-rounded: 30px;

.btn {
  background-color: $grey;
  color: $white;
  font-size: $btn-size;
  border-radius: $btn-radius;

  &.btn-primary {
    background-color: $color-primary;
  }
  
  &.btn-secundary {
    background-color: $color-secundary;
    color: $black;
  }
  
  &.btn-small {
    font-size: $btn-size-small;
  }
  
  &.btn-large {
    font-size: $btn-size-large;
  }
}
```

# Problemas
Deixar mais atômico: Ao invés de dar um @extend com 5 propriedades , podemos criar 5 classes diferentes(DEPENDENDO MUITO DO CASO).

# Liberdade atômica

## Caso 1
```css
.margin-10 {
  margin: 10px;
}

.margin-top-10 {
  margin-top: 10px
}

.margin-right-10 {
  margin-right: 10px
}

.margin-bottom-10 {
  margin-bottom: 10px
}

.margin-left-10 {
  margin-left: 10px
}
```
```html
<div class="margin-top-10">Margin ao topo</div>
<div class="margin-right-10">Margin a direita</div>
<div class="margin-bottom-10">Margin em baixo</div>
<div class="margin-left-10">Margin a esquerda</div>
<div class="margin-top-10 margin-left-10">Margin ao topo e a esquerda</div>
<div class="margin-10"></div>
```

## Caso 2
```scss
.container {
  display: flex
}

.align-items-center {
  align-items: center
}

.justify-content: center {
  justify-content: center
}

@mixin align-content-center() {
  display: flex;
  align-items: center;
  justify-content: center;
}

.align-center {
  @extend align-content-center();
}
```
```html
<div class="align-center"></div>
<div class="container align-items-center justify-content"></div>
```

## Links
- http://rscss.io/
- http://bradfrost.com/blog/post/atomic-web-design/
- https://medium.com/re-write/the-unicorn-workflow-design-to-code-with-atomic-design-principles-and-sketch-8b0fe7d05a37
- https://github.com/bradfrost/patternlab/blob/master/css/style.scss
