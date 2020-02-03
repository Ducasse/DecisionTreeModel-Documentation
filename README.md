# Decision Tree Learning Models

Everyday we try to make decisions about actions we will take. These usually can be structures in a series of conditions, for example "I can go to the party only if I dont have homework for tomorrow. If I don't have homework I will only go if my friends are also going". These conditions seem very intuitive and are very easy to follow, and it can be made even more clear if we show it in the following style

`Put party diagram`

This type of diagram is called a "Decision Tree" since we have a root node at the top and if we follow each node's decision we can end up at a feaf node with a decision that was made. Here we will see how these trees can built and how we can learn these tree structures from labeled data.

## Decision Trees

Just like we showed before, decision trees are a way to represent knowledge on a subject and to arrive to conclusions based on the data that is given. This is done by taking a decision at each node, follow that child, take another decision at the child node and so on. We continue until we get to a 'leaf node', which contains the conclusion that was taken. 

This structure is highly flexible and can be made to work in different type of data, as long as at each node we can make a finite number of decisions then a decision tree can me made. Nonetheless, a very common type of decision tree consists on only making binary choices at each node. This is the case in the party example we saw above. This type of tree can easily adapt to numerical data by using threshold vaules

`Put binary diagram`

Another structure for these trees is to allow each node to have many childs. With this type of tree we can easily model categorical data. Note that it is also posible to adapt `binary diagram` to this type of decision tree model is we decide to create intervals for our values and treat each interval as a category.

`play tennis diagram`
`binary as category diagram`

## Decision tree model

Now that we have seen decision trees we will procede to show how we can learn this structure from labeled data. Let's say we want to learn a model to decide if we should go to play tennis or not, just like in `play tennis diagram`, and for this we have previous data of the decisions we made in the past and under which circumstances these were made.

|    | outlook | temperature | humidity | wind   | play tennis |
|----|---------|-------------|----------|--------|-------------|
| 1  | sunny   | high        | high     | weak   | no          |
| 2  | sunny   | high        | high     | strong | no          |
| 3  | cloudy  | high        | high     | weak   | yes         |
| 4  | rainy   | medium      | high     | weak   | yes         |
| 5  | rainy   | low         | normal   | weak   | yes         |
| 6  | rainy   | low         | normal   | strong | no          |
| 7  | cloudy  | low         | normal   | strong | yes         |
| 8  | sunny   | medium      | high     | weak   | no          |
| 9  | sunny   | low         | normal   | weak   | yes         |
| 10 | rainy   | medium      | normal   | weak   | yes         |
| 11 | sunny   | medium      | normal   | strong | yes         |
| 12 | cloudy  | medium      | high     | strong | yes         |
| 13 | cloudy  | high        | normal   | weak   | yes         |
| 14 | rainy   | medium      | high     | strong | no          |





