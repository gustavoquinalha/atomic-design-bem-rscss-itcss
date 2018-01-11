# Atomic Design + RSCSS
> http://rscss.io/ | http://bradfrost.com/blog/post/atomic-web-design/
> https://medium.com/re-write/the-unicorn-workflow-design-to-code-with-atomic-design-principles-and-sketch-8b0fe7d05a37

- Átomo (Items do styleguide/Variáveis)
- Molécula (Styleguide)
- Organismo (Micro-componentes)
- Template (Componente)
- Pages (Pàgina)

![Image](http://atomicdesign.bradfrost.com/images/content/instagram-atomic.png)

# Plano A

## Tree

- assets
  - css
    - main.scss
    - styleguide
      - _colors.scss
      - _fonts.scss
      - _inputs.scss
      - _buttons.scss
      - _base.scss
    - components
      - _menu.scss
      - _footer.scss
      - _login.scss
      - _card.scss
      - _title.scss
      
### Code
_colors.scss
```scss
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
# Plano B 

## Tree
- assets
  - css
    - main.scss
    
### Code
Variáveis(Atomos)
```scss
// base
$size: 1200px;

// colors
$color-primary: #0081ff;
$color-secundary: #ff4455;

// buttons style
$btn-size-small: 22px;
$btn-size: 32px;
$btn-size-large: 42px;
$btn-radius: 4px;
$btn-rounded: 30px;
```

Styleguide(Molécula)
```scss
@mixin btn-small() {
    font-size: $btn-size-small;
    font-weigth: 400;
}

@mixin btn-normal() {
    font-size: $btn-size;
    font-weigth: 400;
}

@mixin btn-large() {
    font-size: $btn-size-large;
    font-weigth: bold;
}

@mixin btn-primary() {
    background-color: $color-primary;
    color: #fff;
}

@mixin btn-secundary() {
    background-color: $color-secundary;
    color: #000;
}

@mixin align-center() {
    align-items: center;
    justify-content: center;
}
```

Organismo
```scss
.size {
  width: $size;
  max-width: 100%;
  margin: 0 auto;
}

.btn {
  @extend btn-normal();

  &.btn-primary {
    @extend btn-primary();
  }
  
  &.btn-secundary {
    @extend btn-secundary();
  }
  
  &.btn-small {
    @extend btn-small();
  }
  
  &.btn-large {
    @extend btn-large();
  }
}
```

Componente
```scss
.container-header {
  /* ... */

  > .title { /* ... */ }
  > .subtitle { /* ... */ }
  > .paragraph { /* ... */ }
  > .image { /* ... */ }
  > .button {
      .btn { /* ... */ }
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
