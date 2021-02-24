---
layout: post
title:      "Recursion"
date:       2020-11-4 09:57:48 +0000
---

Recursion is when a function calls itself either directly or indirectly. You can solve a problem using recursion if it can be broken down into smaller problems that can be solved using the same steps. An example of this is a prompt called ‘recursion-total-sales.’ This function takes in an object of unknown size, but it could be nested with an employee being a manager of a team and then an employee in that team also being a manager. From the prompt:  `totalSales` accepts one argument, an object containing an employee who manages a sales team, and returns the total sales for the entire team. Note: it is possible that any employee also manages a team.

Because of the nesting in the object, it is a great candidate for recursing over deeper and deeper until the base case is found. The base case is hit in this example when the length of the ‘manages’ array hits 0. The next bigger case after the base case is one of the person objects that may or may not have a ‘manages’ array. As the for loop goes through each of the person objects, the total is added to by a recursive call to the totalSales function. Then when the for loop finishes with all the objects in that ‘manages’ array, the individual sales of the person is added to the total and the total is returned. Once all of the individuals in the object have been ‘visited,’ all the ‘totals’ from the stack of recursive calls get returned one by one and end up as one sales total.

```
var totalSales = function (salesTeam) {
  var total = 0;

  if (salesTeam.manages.length > 0) {
    for (var i = 0; i < salesTeam.manages.length; i++) {
      total += totalSales(salesTeam.manages[i]);     <--- recursive call passing in the person object
    }
  }
  total += salesTeam.individualSales;

  return total;
};
```

Example SalesTeam object:
```
var salesTeam = {
   name: 'Arnaldo McDermott',
   individualSales: 14,
   leadsInProgress: 10,
   manages: [
       {
       name: 'Lavina Romaguera',
       individualSales: 15,
       leadsInProgress: 22,
       manages: [
         {
           name: 'Glen Hodkiewicz',
           individualSales: 12,
           leadsInProgress: 10,
           manages: []
         }
       ]
     },
     {
       name: 'Rey Hills',
       individualSales: 19,
       leadsInProgress: 5,
       manages: []
     }
   ]
 };
```