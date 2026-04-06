---
title: Power Function Explorer
theme: [wide]
header: false
footer: false
sidebar: false
toc: false
---

<style>
  article { display: flex; flex-direction: column; align-items: center; }
  article > * { width: 100%; max-width: 800px; }
</style>

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
  const size = Math.min(width, window.innerHeight - 160);
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
          const y = a * Math.pow(x, n);
          return {x, y: (isFinite(y) && y >= -5 && y <= 5) ? y : NaN};
        }),
        {x: "x", y: "y", defined: (d) => !isNaN(d.y), stroke: "steelblue", strokeWidth: 2.5}
      )
    ]
  });
  svg.style.display = "block";
  svg.style.margin = "0 auto";
  return svg;
})
```
