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
$color-primary: #0081ff;
$color-secundary: #ff4455;

$btn-size-small: 22px;
$btn-size: 32px;
$btn-size-large: 42px;

$size: 1200px;
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
    color: #fff
}

@mixin btn-secundary() {
    background-color: $color-secundary;
    color: #000
}
```

Organismo
```css
.size {
  width: $size;
  max-width: 100%;
  margin: 0 auto
}

.btn {
  /* ... */
  
  > .icon { /* ... */ }

  // variants
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
