# λ-calculus Parser (using LALRPOP)

```rust
use lalrpop_lambda::lambda::ExpressionParser;
let parser = ExpressionParser::new();

// Parse a single free variable.
let x = parser.parse("x");

// Parse the identity function.
let id = parser.parse(r"\x.x");

// f ∘ g
let compose = parser.parse(r"\f.\g.\x.(f (g x))"));

// Print the free variable in this expression.
let unbound_y = parser.parse(r"\x.x y");
println!("{}", unbound_y.free_variables());

// No need for parsing strings at all.
let id = λ!{x.x};
let one = λ!{f.λ!{x.γ!(f, x)}};

// Identity application.
let id = λ!{x.x};
println!("(id one): {} -> {}",
         app!({&id}, {&one}),
         app!({&id}, {&one}).normalize(false));

// Make the Y combinator.
let ω = parser.parse(r"λx.(x x)");
let Ω = parser.parse(r"(λx.(x x)) (λx.(x x))");
let W = parser.parse(r"λf.λx. f x x");
let Y = parser.parse(r"λf.(λx.f (x x)) (λx.f (x x))");
```
