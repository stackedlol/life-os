---
tags: programming
---

### what are decision trees?
- fall under [[supervised-learning]]
- ***splits*** data at each node into separate classes or predict values to make the ***best decision*** at each node

### how are decision trees structured? 
- **root node:** the starting prompt

- **decision nodes:** the intermediate points where decisions are made based on conditions

- **leaf nodes:** the endpoints of the tree where the final classification or regression output is assigned

### how data is split with decision trees?
1. gini impurity (for classification)
	- measures how "pure" a node is (if it belongs to a class)
	- high gini = more mixed groups or classes, less pure
	- lower gini = a purer subset

2. entropy (information gain)
	- measures uncertainty before and after a split 
	- high entropy = high uncertainty 
	- helps make data as predictable as possible

3. mean squared error (MSE)
	- used when predicting numeric values (house)
