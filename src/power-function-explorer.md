---
title: Power Function Explorer
---

# Power Function Explorer

Explore the function **f(x) = a · xⁿ** by adjusting the sliders below.

```js
const a = view(Inputs.range([-5, 5], {value: 1, step: 0.1, label: "a"}));
```

```js
const n = view(Inputs.range([-4, 8], {value: 2, step: 1, label: "n"}));
```

```js
resize((width) => {
  const size = Math.min(width, 900);
  const svg = Plot.plot({
    title: `f(x) = ${a} · x^${n}`,
    width: size,
    aspectRatio: 1,
    x: {domain: [-5, 5], label: "x", grid: true},
    y: {domain: [-5, 5], label: "f(x)", grid: true},
    marks: [
      Plot.ruleY([0]),
      Plot.ruleX([0]),
      Plot.line(
        Array.from({length: 1000}, (_, i) => {
          const x = -5 + i * (10 / 999);
          return {x, y: a * Math.pow(x, n)};
        }).filter(d => isFinite(d.y) && d.y >= -5 && d.y <= 5),
        {x: "x", y: "y", stroke: "steelblue", strokeWidth: 2.5}
      )
    ]
  });
  svg.style.display = "block";
  svg.style.margin = "0 auto";
  return svg;
})
```
