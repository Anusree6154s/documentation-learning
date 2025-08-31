# Basic operators 

* **Terms**

  * **Operand**: value an operator works on (`5 * 2` → operands are 5 and 2).
  * **Unary**: one operand (`-x`). **Binary**: two operands (`y - x`).

* **Math operators**

  * `+` add, `-` subtract, `*` multiply, `/` divide,
  * `%` **remainder** (5 % 2 → 1),
  * `**` **exponent** (2 \*\* 3 → 8; square root: `4 ** 0.5` → 2).

* **String concatenation**

  * Binary `+` also joins strings.
  * If **either** side is a string, the other is converted:
    `'1' + 2 → "12"`, `2 + 2 + '1' → "41"`.

* **Numeric conversion**

  * **Unary `+`** converts to number: `+'42' → 42`, `+true → 1`, `+'' → 0`.
  * Handy for turning form inputs (strings) into numbers.

* **Precedence (what runs first)**

  * Higher runs first: unary `+/-` (14) > `**` (13) > `* /` (12) > `+ -` (11) > `=` (2).
  * Parentheses beat everything.

* **Assignment**

  * `=` returns the assigned value: `let c = (a = 3) - 3;` // `a=3`, `c=0`.

* **Chaining assignments**

  * `a = b = c = 4` evaluates **right→left**; all become 4.

* **Modify in place**

  * `+= -= *= /=` etc.: `n *= 3 + 5` // right side first, then multiply.

* **Increment / Decrement**

  * `++` / `--` only on variables.
  * **Prefix** returns new value: `let a=1; ++a` → 2.
    **Postfix** returns old value: `let a=1; a++` → returns 1 (but `a` becomes 2).

* **Bitwise** (rare in web UIs)

  * `& | ^ ~ << >> >>>` operate on 32-bit integer bits.

* **Comma operator `,`**

  * Evaluates multiple expressions; result is **last** one:
    `let a = (1+2, 3+4); // 7`
  * Very low precedence; often needs parentheses.