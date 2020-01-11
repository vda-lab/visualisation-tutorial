---
title: Advanced interaction
keywords: vega
sidebar: vega_sidebar
permalink: vega-advanced-interaction.html
folder: vega
---
Vega uses the _reactive_ paradigm for interactivity. In reactive programming, the whole of the program is constantly re-evaluated: if a variable changes all other variables that depend on it are _automatically_ updated. This is in contrast to non-reactive programming, where we have to run those dependent variables again.

For example in non-reactive programming:

```ruby
a = 2
b = 3
c = a + b ; c is 5
a = 9
; => c is still 5
```

In reactive programming:

```ruby
a = 2
b = 3
c = a + b ; c is 5
a = 9
; => c is now 12!
```

It's a bit like cells in an Excel sheet that change dynamically if any of the referenced cells change value: like a cell that has the formula `=SUM(A3:A5)` which value changes when we enter a new value in cell `A3`.

<img src="{{ site.baseurl }}/assets/vega-excel.png" width="50%" />

The OpenVis talk at [https://www.youtube.com/watch?v=Y8Fp9z-9DWc](https://www.youtube.com/watch?v=Y8Fp9z-9DWc) describes the system in detail. Much of the following is taken from that talk and the [corresponding paper](http://idl.cs.washington.edu/files/2014-DeclarativeInteraction-UIST.pdf). See also [Satyanarayan's UIST talk](http://vis.csail.mit.edu/pubs/reactive-vega-model).

In the static images we created above, we had to define the `data`, `transforms`, `scales`, `guides` and `marks`. Similarly, the following concepts apply when talking about interaction.

| Static     | Dynamic          | Example                                               |
|:---------- |:---------------- |:----------------------------------------------------- |
| data       | event streams    | `[mousedown, mouseup] > mousemove`                    |
| transforms | signals          | `minX = min(width, event.x)`                          |
| scales     | scale inversions | `minVal = xScale.invert(minX)`                        |
| guides     | predicates       | `p(t) = minVal =< t.value =< maxVal`                  |
| marks      | production rules | `fill = p(t) -> colorScale(t.category) ; nil -> grey` |
