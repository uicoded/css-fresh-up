# Cascade

CSS stands for Cascading Stylesheets. The cascade is the algorithm for solving conflicts where multiple CSS rules apply to an HTML element.

The cascade algorithm is split into 4 distinct stages.

1. **Position and order of appearance**: the order of which your CSS rules appear
2. **Specificity**: an algorithm which determines which CSS selector has the strongest match
3. **Origin**: the order of when CSS appears and where it comes from, whether that is a browser style, CSS from a browser extension, or your authored CSS
4. **Importance**: some CSS rules are weighted more heavily than others, especially with the `!important` rule type