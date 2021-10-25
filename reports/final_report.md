# Robustness of Complex Graphs with Random Failures and Targeted Attacks
### Will Fairman and David Tarazi

## Abstract
Albert, Jeong, and Barabasi explore the robustness of different complex graphs by looking at two specific types of failure: removing random nodes and systematically removing nodes with the highest degree. With small rates of failure, the authors use the average shortest path length as a characteristic of robustness. With high rates of failure, where a graph is likely to become disconnected, the authors instead associate robustness with the percentage of nodes that are in the largest connected cluster, representing the percentage of nodes that are still reachable. To expand upon the paper, we implemented random edge removal as another way to attack these complex graphs and evaluate their robustness.  While the authors specifically compared the Erdos and Renyi (ER) random graph model and the Watts and Strogatz (WS) small world model, we expanded the robustness analysis by looking at two real-world data sets: the facebook social network (a known small-world graph) and a graph representing the power grid of the Western United States (IS THIS RIGHT?).



## Introduction
By comparing different graph models and their properties in response to random attacks or failures, we can determine which types of models would be best for different applications. For example, in the design of an electrical grid, maintaining a connected graph is more important than the shortest path length between any two nodes. Alternatively, in the design of a road network, the shortest path between any two nodes representing cities or locations in a city is probably an important consideration, especially if the edges are weighted and there can be an analysis of how long it would take to traverse from one node to another.

In an attempt to draw failure characteristics from real-world graphs, we used the Facebook Social Network data to represent a small-world graph and data from a Power grid which we will later associate with an exponential, Erdos Renyi, graph. 

 unlike the WS model, the degree distribution is long-tailed and has a much greater range.

 ```
 talk about how the Facebook and Power Grid data compare to the WS and ER graphs?
 
 ```

The results suggest that random graphs like the ER model are more robust than small world graphs like the WS model in most, but not all aspects. We noticed that with small fractions of failures or targets, the random graph is just as robust to targeted node attacks and random node and edge attacks. However, the random graphs tend to lose the connected property earlier than the small world graphs. At scale, we noticed that the relative size of the largest cluster for random graphs stays much higher than the small world graphs with random deletion of nodes and edges, but with targeted attacks, we observe that the random and small world graphs both tend to have a critical failure point where the largest cluster size decreases rapidly at around 20-30% of total node removal. Furthermore, when applying the attacks to the Facebook model, we observe that the nodes with a significantly high degree fail early and the robustness of the graph is less than both other models we analyzed.

## Experiment
In our exploration, we will replicate some of the experiments that Albert, Jeong, and Barabasi conducted while extending this application to a real world example. In our replication, we will implement two graphs: a Watts and Strogatz (WS) model that the authors refer to as scale free and a Erdos and Renyi (ER) random model which the authors refer to as an exponential graph. For both of these models, we use a node and edge count the authors use in the paper: 10,000 nodes, 20,000 edges. When analyzing these, we will look at the average shortest path length for both graphs as we remove nodes. We will also evaluate the size of the largest cluster along with the average size of the isolated clusters as the graph disconnects over enough failures/attacks. 

After implementing these tools, we then expand our types of attacks to include random edge removal. This investigation is interesting for the potential applications into real world models. For example, if a power line is severed during a storm, power may be cut off between a town and a power substation. In this case, removing a node (representing a substation) would not properly reflect this type of failure. Once we have expanded our analysis tools, we will look at a model we downloaded for an electrical grid in order to analyze the electrical grid’s robustness to both random failure (as if during a bad storm) and attacks on that grid. Throughout the experiment, we also test the robustness of the a Facebook data set: a real-world representation of a small-world graph.

## Results

### Average Shorest Path Length
The following figure shows the results from Albert, Jeong, and Barabasi's experiment on exponential grapHoweverhs (ER) and scale-free graphs (WS). The x-axis reflects the percentage of the nodes removed during the attack while the y-axis shows the diameter, average shortest path length, of the graphs. For both types of graphs, the authors used a node size of 10,000 and an edge count of 20,000. In Figure 1, the authors plotted the average path length between any two nodes as the ratio of removed nodes to starting nodes increased. 

![pathlengthReplication](figures/projectproposal2.png)

**Figure 1:** Graph from Albert, R., Jeong, H. & Barabási, AL that shows average path length of exponential (ER) and scale-free (WS) networks. The x-axis is the fraction of nodes removed. The y-axis is the average shortest path length. Two types of attacks are applied. The first is a random node removal labeled as "Failure" and the second is a targeted node removal labeled "Attack".

The next figure shows our implementation of the authors' work. While our shortest path lengths are offset by about 10, the general characteristics of the graphs hold. The exponential (ER) graph shows little difference when under a random or targeted attack. However, the scale-free graph's (WS) path lengths increase at a much faster rate when nodes with a larger degree are removed.

![pathLengthReplicationUs](figures/fig2.jpg)

**Figure 2:** Replication of average path length graph shown in Figure 1. Nodes are removed randomly and targeted with a WS and an ER graph both with 10,000 nodes and 20,000 edges. The WS probability of rewiring is 0.05.

Figures 1 and 2 suggest that when minimal attacks or failures occur, random graphs tend to be more resilient and hold their average shortest path length between any two nodes when compared to a small world graph model. There is one flaw that isn't represented well in Figures 1 and 2. The random graph generally holds the average shortest path length, but it is more likely to have a failure that results in a node losing connection to the main cluster at a lower percentage of removed nodes. To see a comparison to real-world data, we also plotted the Facebook and Power Grid dataset. As you can see below, the starting shortest path length is much smaller than our previous examples. This is also attributed to the much larger edge to node ratio in the Facebook data. To better reflect this difference, we plotted WS and ER graphs in Figure 3 that have the same number of nodes and edges as the Facebook and Electrical Grid data respectively.

 The Facebook graph, however, still reflects most of the characteristics of our original scale-free graph. A random attack has almost no affect on the path length while the targeted attack nearly doubles the average path length in the first round followed by an overall steeper slope. The removal of the few "most popular" people in this graph model doubles the number of people you are away from any other person, so keep your popular friends safe! 

 ```
 Talk about Electrical Grid Characteristics
 
 ```

![pathLengthfb](figures/fig3.jpg)

**Figure 3:** Path Length characteristics our Facebook and Power Grid dataset. The Facebook data and respective WS graph have 4,039 nodes and 88,324 edges respectively. The Electrical Grid and respective ER graph have 4,941 nodes and 6,594 edges.


### Cluster Size
The next characteristic the authors observed was the average isolated cluster size and relative largest cluster size. An isolated cluster is defined as any cluster that is not part of the largest cluster and the average isolated cluster size is the average number of nodes in all of the isolated clusters. The relative largest cluster size is the size of the largest cluster normalized by the total number of nodes left in the network. The following diagram shows the author's results when plotting these characteristics from their ER and WS graphs.

![clusterReplication](figures/projectproposal1.png)

**Figure 4:** Paper's average clustering as nodes are removed randomly and targeted. The figure also shows real-world data sets used by the authors to reflect small-world and exponential graphs.

Figure 4 is a little difficult to interpret. Essentially, the results from Albert, Jeong, and Barabasi suggest that at scale, small world models tend to have a higher relative largest cluster size even as many nodes are removed on a linear relationship with random removals when compared to random graphs, but small world graphs fail quicker when there is a targeted attack (as shown in the top row of the figure). Our results begin to diverge with the authors' when calculating the isolated cluster size and largest relative cluster. When looking at the relative largest cluster size, both the expontential and scale-free graphs stay close to 1 until hitting a critical percentage of nodes removed and drop rapidly towards 0. For the exponential graph this is expected behavior in both the random and targeted attacks as eventually the central node is spread thin and splits into many smaller clusters. This relation also holds true for the scale-free network under a targeted attack. However, the authors suggest that the largest cluster size of the scale free graph should decrease linearly under a random attack. This does not align with our graph which shows a fairly steep decline in the graph's cluster size around 20-30% of the nodes removed. Our results imply that random graphs hold their largest cluster much more effectively than small world graphs under a random attack, but under a targeted attack, the two models are similar in how they hold their largest cluster size.

The average isolated cluster size differs even more when comparing to the paper's original graph. For an exponential graph, the paper shows a spike in isolated cluster sizes around the critical point in which the largest cluster size falls rapidly. Under a random attack, we do not see a spike in isolated cluster sizes. However, we also don't see a critical point within the range plotted. This could suggest that this spike does occur, but not in this sample of data collected. There is a spike in isolated cluster sizes when an exponential graph experiences targeted attacks: also lining up with the critical point where cluser size drops. This relationship also holds true for the scale-free graph under a targeted attack. According the paper, the scale-free graph should not see a spike in isoalted clusters during a random attack because there is no crictical point at which the largest cluster size falls. Because we see this critical point in our own data, we also see a spike in isolated clusters. One major difference between the exponential and small world models is that the exponential models often have clusters that end up having just a single isolated node or many of them as the removal continues. On the other hand, the average isolated cluster size appears to grow significantly until a certain point (or spike) in the small world model. This growth implies that the small world model ends up splitting into many clusters of a much larger size than the random graph so those clusters could stay connected where the random graph may isolate individual nodes much more often. In a cellular communication network for instance, it may be advantageous to have these smaller clusters appear as most people don't need to call outside of their immediate area as failures occur. While the random graph appears much more robust, there are advantages to both models depending on what the network is attempting to optimize.

![clusterReplicationUs](figures/fig5.jpg)

**Figure 5:** Average isolated cluster size and relative cluster size plotted for our ER and WS graphs with nodes=10,000 and edges=20,000 with probability of rewiring = 0.05 in the WS graph.

Again, we used the Facebook dataset to compare our results with a real-world small world graph. The characteristics of the Facebook data closer resemble the results we produced rather than the expected results from paper.

![clusterReplicationfb](figures/fig6.jpg)

**Figure 6:** Average isolated cluster size and relative cluster size plotted for Facebook Electrical Grid data. WS and ER graphs are also plotted with the same node and edge count as the Facebook and Electrical Grid data respectively.

### Random Edge Removal
Beyond just random node removal, we implemented a random edge removal. The following figure shows our exponential and random graphs' response to this type of attack. We also plotted the response of these graphs to all of the attacks mentioned previously. The randome edge removal behaves fairly similar to the random node attack. Following the pattern of random node removal, the random graph appears to be the most robust to any type of attack on the system. 

![edgeRemoval](figures/fig7.jpg) 

**Figure 7:** All three types of attacks plotted against all three types of robustness characteristics. ER and WS graphs with 10,000 nodes and 20,000 edges were used.

Again, we plotted a random edge attack on the Facebook dataset to see how a real-world graph is effected by the this type of attack. As anticipated, we observed that the Facebook dataset acts very similarly to the Watts-Strogatz graph. The issue of the Facebook model's larger degree distribution doesn't show in this attack though since the removal is random and not targeted.

![edgeRemovalfb](figures/fig8.jpg)

**Figure 8:** All three types of attacks plotted against all three types of robustness characteristics for the Facebook and Electrical Grid data. WS and ER graphs are also plotted with the same node and edge count as the Facebook and Electrical Grid data respectively.
 

## Causes of Concern
One cause of concern that we had is that our results didn't match the results of Albert, Jeong, and Barabasi as closely as we anticipated. We worry that the way we implemented their experiment doesn't match the actual experiment that they conducted. Although we are concerned with this discrepency, we are fairly certain that our implementation accurately analyzes robustness in graphs. 

Another cause of concern or rather a question that we pose for further exploration would be how do you implement a targeted edge removal? We considered targeting edges from the most connected node or targeting edges from the least connected node to explicitly cause the graph to lose its connected property, but we couldn't determine a real application where this data would provide greater insight into determining which graph to use solely on its robustness.

Finally, we are concerned that we haven't explored how to choose which model is best to follow when trying to design a system and we wonder if we have provided enough information given just these few models to determine which graph to choose. In the future, it would be interesting to explore more complex models and how they respond to these attacks. It's possible that there are better options that still achieve the functionality that users are looking for when designing networks. For others exploring this field, we would challenge you to explore different models and think about how to model graphs through a lens of robustness.

## Our Next Steps
Will and I plan on testing different networks such as an electrical grid and we hope to look into potentially exploring another type of model if we end up having the time to do so. We feel confident in our results thus far, but we will also be checking our experiments to see if we can find where the discrepency between our results and the paper we followed's experiments lies.

## Annotated Bibliography
[Error and Attack Tolerance of Complex Networks](https://www.nature.com/articles/35019019.pdf?origin=ppub)  
Albert, R., Jeong, H. & Barabási, AL. Error and attack tolerance of complex networks. Nature 406, 378–382 (2000). https://doi.org/10.1038/35019019
>This paper discusses some of the implications of random and targeted attacks on ER and WS graphs (as well as an Internet model) in order to quantify their robustness to these attacks.

[Western US States Power Grid Network Model](http://konect.cc/networks/opsahl-powergrid/)
>This model represents the Western US States’ power grid that we plan to use for our experimentation. The nodes are transformers, substations, and generators, and the edges are high-voltage transmission lines.
