---
title: Power Function Explorer
theme: [wide]
---

# Power Function Explorer



```tex
f(x) = ${a} · x^{${n}}
```

```js
const a = view(Inputs.range([-5, 5], {value: 1, step: 0.1, label: "a"}));
```

```js
const n = view(Inputs.range([-4, 8], {value: 2, step: 1, label: "n"}));
```

```js
resize(w => Plot.plot({
  width: Math.min(w, window.innerHeight - 160),
  aspectRatio: 1,
  x: {domain: [-5, 5], label: "x", grid: true},
  y: {domain: [-5, 5], label: "f(x)", grid: true},
  marks: [
    Plot.ruleX([0]),
    Plot.ruleY([0]),
    Plot.line(
      Array.from({length: 1000}, (_, i) => {
        const x = -5 + i * 10 / 999
        const y = a * x ** n
        return {x, y: (isFinite(y) && y >= -5 && y <= 5) ? y : NaN}
      }),
      {x: "x", y: "y", defined: d => !isNaN(d.y), stroke: "steelblue", strokeWidth: 2.5}
    )
  ]
}))
```
