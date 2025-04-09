## Your change log

### bugs/errors

- changed change log name for clarity
- fixed syntax in product.json
- add semicolon to line 29 of app.vue to correct error
- corrected product.json path name in product.vue

### Build

I have used a mix of css and bootstrap utility classes to put the page styling in line with the design.

The sizing and colour sections are produced using v-for elements interating through the arrays provided in the JSON.

Custom methods provide the logic for the offer percentage and add to bag alert. The alert box provides a "violation 'click' handler took Xms" warning in the console as alert is process blocking, I've kept the code as it functions and an alert box was specified in the readme.

I worked with responsiveness in mind throughout the process so in order to ensure full responsiveness I only had to add some media queries and change the styling units on the size section to ensure they wrapped for different screen sizes.
