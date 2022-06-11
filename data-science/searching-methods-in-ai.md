# Searching methods in AI

* Tree vs. Graph from AI strategy perspective. What is the difference?&#x20;
  * Tree search does not keep a record of previously explored frontiers/ nodes, whereas a graph search does keep a record of this
* Search algorithm performance metrics. What factors should we consider?
  * whether the algorithm is _complete_ (guaranteed to find a solution)
  * we want to find the best possible solution (_optimality)_
    * best cost possible&#x20;
  * two factors to consider for any algorithm (comp sci 101)
    * Time complexity - how long&#x20;
    * Space complexity - how much memory

## Uninformed search (blind)

* Breadth first search
  * What kind of data structure do you use for BFS? (How do you start visiting the nodes?)&#x20;
  * FIFO = queue
* Uniform cost search
* Depth first search
* Depth limited search
* Iterative deepening search
* bidirectional search&#x20;

## Informed search (heuristic)&#x20;

* Best first search
* Greedy best first search
* A\* search
* Iterative deepening A\* search&#x20;
