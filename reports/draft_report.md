# Robustness of Complex Graphs with Random Failures and Targeted Attacks
### Will Fairman and David Tarazi

## Abstract
Albert, Jeong, and Barabasi explore the robustness of different complex graphs by looking at two specific types of failure: removing random nodes vs removing nodes with the highest degree. With small rates of failure, the authors use the average shortest path length as a characteristic of robustness. With high rates of failure, where a graph is likely to become disconnected, the authors instead associate robustness with the percentage of nodes that are in the largest connected cluster: representing how much of a network is still usable. This paper specifically compared the Erdos and Renyi (ER) random graph model and the Watts and Strogatz (WS) small world model. We have generated both types of graphs using networkX and are planning on using the python library for this experiment as well. As an extension to the author's paper, we will explored the robustness of these networks to a new kind of attack: random edge removal. We will also apply the tools we create to anaylze robustness on real world networks (power grids, road networks) to determine what type of failure modes these graphs are susceptible to.

## Experiment
In our exploration, we will replicate some of the experiments that Albert, Jeong, and Barabasi conducted while extending this application to a real world example. In our replication, we will implement two graphs: a Watts-Strogatz Scale Free Network, and an ER Exponential Network following their size and number of edges. We then will conduct a random attack on the nodes as well as a targeted attack on the most connected nodes. When analyzing these, we will look at the average shortest path length for both graphs as we remove nodes. We will also evaluate the size of the largest cluster along with the average size of the isolated clusters as the graph disconnects over enough failures/attacks. We hope that we can find the critical failure value where these networks become disconnected.

After implementing these tools, we will expand our types of attacks to include random edge removal. This could be an interesting analysis as it draws similiraties to failures in real-world graphs. For example, if a power line is severed during a storm, power may be cut off between a house and a power substation. In this case, removing a node (house, substation) would not properly reflect this type of failure. 

Once we have expanded our analysis tools, we will look at a model we downloaded for an electrical grid in order to analyze the electrical grid’s robustness to both random failure (as if during a bad storm) and attacks on that grid.

## Results

### Average Shorest Path Length
The following figure shows the results from Albert, Jeong, and Barabasi's experiment on exponential graphs (ER) and scale-free graphs (WS). The x-axis reflects the percentage of the nodes removed durring the attack while the y-axis shows the diameter, average shortest path length, of the graphs. For both types of graphs, the authors used a node size of 10,000 and an edge count of 20,000.

![pathlengthReplication](figures/projectproposal2.png)

**Figure 1:** Paper's Diagram showing path length as nodes are removed randomly and targeted.

The next figure shows our implementation of the authors' work. While our shortest path lengths are offset by about 10, the general characteristics of the graphs hold. The exponential (ER) graph show little difference when under a random or targeted attack. However, the scale-free graph's (WS) path lengths increase at a much faster rate when large nodes are removed.

![pathLengthReplicationUs](figures/fig1_replicated.jpg)

**Figure 2:** Path length replication as nodes are removed randomly and targete

To see a comparison to real-world data, we also plotted the facebook dataset used previously in class. This dataset is an example of a small-world graph with 4,039 nodes and 88,234 edges. As you can see below, the starting shortest path length is much smaller than our previous examples. This is attributed to the much larger edge to node ratio in the facebook data. The facebook graph, however, still reflects the characteristics of our original scale-free graph. A random attack has almost no affect on the path length while the targeted attack nearly doubles the average path length in the first round followed by an overall steeper slope. 

![pathLengthfb](figures/fig1_fb_replicated.jpg)

**Figure 3:** Path Length characteristic of a facebook friends dataset with 4,039 nodes and 88,324 edges.


### Cluster Size
The next characteristic the authors observed was the average isolated cluster size and relative cluster size. An isolated cluster is defined as any cluster that is not part of the largest cluster and the average isolated cluster size is the average number of nodes in all of the isolated clusters. The relative cluster size is the size of the largest cluster normalized by the total number of nodes left in the network. The following diagram shows the author's results when plotting these characteristics from their ER and WS graphs.

![clusterReplication](figures/projectproposal1.png)

**Figure 2:** Average clustering as nodes are removed randomly and targeted.


## Annotated Bibliography
[Error and Attack Tolerance of Complex Networks](https://www.nature.com/articles/35019019.pdf?origin=ppub)  
Albert, R., Jeong, H. & Barabási, AL. Error and attack tolerance of complex networks. Nature 406, 378–382 (2000). https://doi.org/10.1038/35019019
>This paper discusses some of the implications of random and targeted attacks on ER and WS graphs (as well as an Internet model) in order to quantify their robustness to these attacks.

[Western US States Power Grid Network Model](http://konect.cc/networks/opsahl-powergrid/)
>This model represents the Western US States’ power grid that we plan to use for our experimentation. The nodes are transformers, substations, and generators, and the edges are high-voltage transmission lines.
