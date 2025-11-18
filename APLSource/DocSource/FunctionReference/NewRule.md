# NewRule

Creates a new CSS rule.

~~~
R←{Y} NewRule X
~~~

`X` is the selector.
`Y` is an optional parent (for CSS nesting).
`R` is a new rule object.

## Examples

~~~
      r←A.NewRule 'h1'
      r
CSSRule
      r.font_size←'2rem'
      r.padding←'.5rem'
      A.ComposeRules r
h1 {
    font-size: 2rem;
    padding: .5rem;
}
~~~
