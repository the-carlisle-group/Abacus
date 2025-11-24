# CSSRule NewRule Method

Create a new CSSRule.

~~~
      R←{I} NewRule X
~~~

`X` is the selector. I in an optional parent CSSRule.
R is a new CSSRule instance.

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
