# Device size specific CSS

```
@media only screen and (max-width: 700px) {
  /*.ui.fixed.menu {
    display: none !important;
  }*/
  .secondary.pointing.menu .item,
  .secondary.pointing.menu .menu {
    display: none;
  }
  .secondary.pointing.menu .toc.item {
    display: block;
  }
  .masthead.segment {
    min-height: 350px;

  }
  .masthead h1.ui.header {
    font-size: 2em;
    margin-top: 1.5em;
  }
  .masthead h2 {
    margin-top: 0.5em;
    font-size: 1.5em;
  }
  .segment h2{
    color: #00296b;
  }
}
```