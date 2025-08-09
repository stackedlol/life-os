---
tags: language
---

### core concepts of CSS
1. ==specificity==:

	- decides which CSS rule "wins" when multiple rules apply to the same element

2. ==box model==:

	- is how every [[html]] element is structured and spaced on a webpage... helps with layout, spacing, and borders

		- ***CONTENT***:
			- the actual text, image, or element content
			- controlled with properties like width/height

		- ***PADDING***:
			- space inside the box around the content
			- makes space between content and border

		- ***BORDER***:
			- wraps around the padding and content
			
		- ***MARGIN***:
			- space outside the box
			- used to push elements apart
	
3. ==layout==:

	- ***FLEXBOX***: one-dimensional layout (row or column)
		- best for aligning items horizontally or vertically
		- dynamic spacing and reordering

	- ***GRID***: two-dimensional layout (rows + columns)
		- good for complex layouts
		- dashboards, galleries, and other full page styles

4. ==positioning==:

	- used to control how and where elements are placed in relation to their parent or the page
		- static - elements flow naturally in the page
		- relative - moves the element relative to its normal position
		- absolute - positions the element relative to the nearest positioned ancestor
		- fixed - sticks the element to the viewport (doesn't move when scrolling)
		- sticky - scrolls like normal, then sticks to a position once it hits it
   
---
### putting these to work...
```css

/* Flexbox to center the box */
.container {
  display: flex;             /* flexbox layout */
  justify-content: center;   /* horizontal center */
  align-items: center;       /* vertical center */
  height: 100vh;             /* full screen height */
}

```

---

