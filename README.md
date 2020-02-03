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

We will see different ways we can build a decision trees for this data.

### ID3 Algorithm

One algorithm that can be used to learn a decision tree from data is called ID3. This algorithm is simple to understand and implement, but one of its downfalls is that it only works for categorical data. We will later see the algorithm C4.5, which extends ID3 to be able to handle numerical data as well as missing data. For now, we will see how ID3 can be used to build a decision tree from the given table.

ID3 can be briefely summerized in the follwing instructions

```
ID3(Training set S, Attributes)
1) Create root node for the tree
2) If all examples in S have the same label, return leaf node with that label
3) If Attributes is empty, return leaf node with most common label
4) Else
5)    Let v <- Atribute that returns best Information Gain
6)    For all posible values, v_j, of v:
7)      Add a new child of root (corresponding to the test v=v_j)
8)      Let Examples(v_j) be the instances of S where v=v_j
9)      If Examples(v_j) is empty
10)        Return leaf node with most common label in the examples
11)      Else
12)       Return ID3(Examples(v_j), Attributes / {v})
```

This is all the ID3 algorithm, in short what the algorithm does is find the attribute that gives the best information gain, split the dataset on that attribute and then repeat for each of its childs using the remaining attributes. We will procede to explain in depth what each step refers to. 

#### Stopping criteria

We can see in step 12 that this algorithm follows a recursive strategy, after each split it will repeat the same process for every child node. This is why we need some conditions to tell the algorithm when to stop and return a value. This conditions are specified in steps 2 and 3. The first condition says that if the dataset S is perfecly label, then you should stop the recursion and return a leaf node with the label. The second condition says that if the set of attributes is empty, then you must return a leaf node with the most common label. This step is important because once we choose an attribute to make a split that attribute will no longer be considered in the rest of the splits coming below it in the hirarchy. This means that it is posible that at one step we will run out of attributes to use. In this case we will say that by default you should return a leaf node with the most common label in the examples.

#### Information Gain

To compare how good is each attribute to split the data we have to define a metric that tells us what a "good" separation is. In this case, our mesure of how mixed or "impure" the dataset labels are will be the entropy of the data. The entropy tries to quantify the level of "surprise" of seeing an output, where unlikely events produce a bigger surprise that likely ones. The formal definition of entropy is as follows:

![equation](https://latex.codecogs.com/png.download?H%28T%29%20%3D%20%5Csum_i%20p_i%20%5Clog_2%28p_i%29)

