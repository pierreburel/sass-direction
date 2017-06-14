# Direction

Sass mixins and functions to help creating bi-directional stylesheets.  

Compatibility: [Sass](https://github.com/sass/sass) and [LibSass](https://github.com/sass/libsass) 

--- 

## Install

Download [`_direction.scss`](https://raw.githubusercontent.com/pierreburel/sass-direction/master/_direction.scss) or install with [npm](https://www.npmjs.com/) or [Bower](http://bower.io/) :

### npm

```
npm install sass-direction
```

### Bower

```
bower install sass-direction
```

---

## Usage

### `app.scss`

```scss
@import "direction";

h1 {
  text-align: direction(left);
  margin-#{direction(right)}: 1em;
  padding: direction-sides(1em 2em 3em 4em);
  border: direction-corners(1em 2em 3em 4em);
  font-size: direction-if(ltr, 1em, 2em);
  line-height: direction-if(rtl, 2);
  flex-direction: direction(row);
  justify-content: direction(flex-start);
  
  @include direction-if(ltr) {
    &::before {
      content: "left to right";
    }
  }
  
  @include direction-if(rtl) {
    &::after {
      content: "right to left";
    }
  }
  
  direction: direction(rtl);
  
  & > span {
    direction: direction(ltr);
  }
}
```

### `app-rtl.scss`

```scss
$direction: rtl;
@import "app";
```

---

## Result

### `app.css`

```css
h1 {
  text-align: left;
  margin-right: 1em;
  padding: 1em 2em 3em 4em;
  border: 1em 2em 3em 4em;
  font-size: 1em;
  flex-direction: row;
  justify-content: flex-start;
  direction: rtl;
}
h1::before {
  content: "left to right";
}
h1 > span {
  direction: ltr;
}

```

### `app-rtl.css`

```css
h1 {
  text-align: right;
  margin-left: 1em;
  padding: 1em 4em 3em 2em;
  border: 2em 1em 4em 3em;
  font-size: 2em;
  line-height: 2;
  flex-direction: row-reverse;
  justify-content: flex-end;
  direction: ltr;
}
h1::after {
  content: "right to left";
}
h1 > span {
  direction: rtl;
}
```

---

## Aliases

- Function `direction-ltr($if, $else)`: `direction-if(ltr, $if, $else)`
- Function `direction-rtl($if, $else)`: `direction-if(rtl, $if, $else)`
- Mixin `direction-ltr`: `direction-if(ltr)`
- Mixin `direction-rtl`: `direction-if(rtl)`

--- 

## Credits

Hugely based on [Tyson Matanich](http://matanich.com)’s [idea](https://github.com/tysonmatanich/directional-scss).
