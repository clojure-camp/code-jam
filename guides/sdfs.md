# Signed Distance Fields

Your task is to learn, implement, and play with 'Signed Distance Fields' in Clojure.

An SDF describes a shape as a function: given a point, it returns the distance to the shape's edge — negative inside, zero on the boundary, positive outside. This one idea powers a lot of modern graphics (shaders, font rendering, 3D ray-marching). Shapes are just functions, thus: moving, scaling, and combining shapes is just function composition!

[This tutorial](https://tutorials.tektite.studio/signed-distance-fields/) is a useful guide. You can either can puzzle through the math for each of the tasks below; or, check out the link for sample code and translate it in to Clojure.

## Set Up

- `git clone https://github.com/clojure-camp/sdfs.git`
- `npm install`
- `npm start`
- open https://localhost:8080
- open in your editor of choice and connect the REPL (shadow-cljs)
- edit `src/sdfs/core.cljs` to have it hot-reload

See the [README](https://github.com/clojure-camp/sdfs) if you run into issues.

## Getting Started

- *Understand the starter code* - The `draw!` function expects to be passed an SDF; for this project, this means a function that takes a vector of x and y coordinates, and returns a number. What does the starter SDF draw? Why does it draw that?

- *Tweak `draw!` to help with debugging* - Instead of a constant black on the inside, replace it with `(str "oklch(70% 30%" (Math/abs distance) ")")` which will set the hue based on the magnitude returned from the SDF. Thus, the hue will indicate how far a given point is from the edge of the drawn shape. This may help with understanding what's going in with the following exercises. Note that the color eventually cycles (because the oklch function happily takes any value for hue). If you prefer, you can use isolines instead: `(if (< -1 (rem distance 25) 1) "#AAA" "#000")`

- *Draw a circle* - change the SDF function to draw a circle of radius 100 from the origin (0,0). What does a circle mean in terms of SDFs? Remember: given an `x` and a `y`, we want to return a negative number if it's inside a circle, and positive if it's outside. (Also, because the origin is at the top left, this will end up drawing a quarter circle - we'll figure out how to move it soon)
  <details>
    <summary>Hint</summary>
    For a circle at the origin, we could check if a point's distance to the origin is less than or greater than the radius.
  </details>
  <details>
    <summary>Hint</summary>
    ...but we don't want a boolean, we want the distance to the edge, so we subtract the radius from the distance.
  </details>

- *Extract a `circle` higher-level function* - The function should take a radius, and return an SDF function. Replace your previous code to use this new function instead.
  <details>
    <summary>Hint</summary>
    It should end up similar to: `(defn circle [r] (fn [[x y]] ,,,))`
  </details>

- *Move the circle* - Create a new `translated-circle` function that also takes a `dx` and `dy` and offsets the circle by those amounts (in other words, `dx` and `dy` act as the origin).

- *Implement `translate`* - Instead of always modifying our shape functions to support translation, we could create a higher-level function that takes an existing SDF and returns a new SDF with some transformation applied. If you know of 'middleware' from web-app development, this is the same idea! The `translate` function should take `dx`, `dy` and `f` (an SDF), and it should return a new SDF. When calling the original SDF (`f`), the `x` and `y` that are passed to it should be modified by `dx` and `dy`. Try to implement `translate` and use it draw a circle away from the origin.

- *Implement `union`* - What if we want to draw multiple shapes? The `union` functions should take any number of sdfs as args. To implement, we can let the 'closest' sdf decide the distance to our unioned surface (by using `min`).


## Extensions

Choose one or more of these, based on your interests:

- implement other basic shapes
  - see [this page](https://iquilezles.org/articles/distfunctions2d/) for formulas
  - `segment` (a line from a to b with thickness r)
  - `rectangle` (and then `square`)
  - `polygon` (of n sides)
- implement other combinators
    - see [Primitive Combinations and below on this page](https://iquilezles.org/articles/distfunctions/) for formulas
    - `rotate`
    - `scale`
    - `mirror`
    - `intersection` (hint: it's the inverse of union)
    - `subtraction`
    - `outline`
    - `fuzz` (adding random noise to x and y)
    - `smooth-union` (see [Smooth Blending in this article](https://tutorials.tektite.studio/signed-distance-fields/))
    - `repeat` (tiled copies)
- recreate the Clojure logo
- animate: render as a function of time

## Super Stretch

Done everything else? Take one or more of these on:

- change draw! to render 3D sdfs
- use the 'marching squares' algorithm to export shapes to an SVG
- port to babashka or jvm clojure, have it output pngs
- write a cross-compiler from our language to GLSL shaders, render with WebGL
