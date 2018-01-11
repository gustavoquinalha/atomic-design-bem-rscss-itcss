# Atomic Design + RSCSS
> http://rscss.io/ | http://bradfrost.com/blog/post/atomic-web-design/

- Átomo (Items do styleguide/Variáveis)
- Molécula (Styleguide)
- Organismo (Micro-componentes)
- Template (Componente)
- Pages (Pàgina)

![Image](http://atomicdesign.bradfrost.com/images/content/instagram-atomic.png)

# Tree

- assets
  - css
    - main.scss
    - variables
      - _colors.scss
      - _sizes.scss
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
      
# Code

Átomo
```css
// base
$size: 1200px;
// colors
$color-primary: #0081ff;
$color-secundary: #ff4455;
// buttons style
$btn-size-small: 22px;
$btn-size: 32px;
$btn-size-large: 42px;
```

Molécula
```css
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
```css
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
```css
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

```css
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

<div class="align-center"></div>
<div class="container align-items-center justify-content"></div>

<div class="margin-top-10">Margin ao topo</div>
<div class="margin-right-10">Margin a direita</div>
<div class="margin-bottom-10">Margin em baixo</div>
<div class="margin-left-10">Margin a esquerda</div>

<div class="margin-10"></div>
```

# Liberdade atômica
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

<div class="margin-top-10">Margin ao topo</div>
<div class="margin-right-10">Margin a direita</div>
<div class="margin-bottom-10">Margin em baixo</div>
<div class="margin-left-10">Margin a esquerda</div>
<div class="margin-top-10 margin-left-10">Margin ao topo e a esquerda</div>
<div class="margin-10"></div>
```
