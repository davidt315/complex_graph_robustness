# Draft Review: [Adding Heterogeneity to the Schelling Model](https://github.com/benmor20/ComplexityProject1/blob/main/reports/draft_report.md)
Will

## Question
**What is your understanding of the experiment the team is replicating?  What question does it answer?  How clear is the team's explanation?**

The team is planning to replicate Schelling's model of segregation including testing additional rules that expand the kernel size (number of neighbors) each household includes in its decision to move. The team also wants to add an additional weight that involves households having a preference for a diverse set of neighbors. The goal of this addition is to figure out the weights that lead to a well-mixed neighborhood. This explanation was succinct and clear. 


## Methodology
**Do you understand the methodology?  Does it make sense for the question?  Are there limitations you see that the team did not address?**

It seems like the team wants to test two variables: size of kernel radius and different acceptable levels of heterogeneity. It's not entirely clear how the team wants to implement heterogeneity. I'm assuming there will be a `too mixed < x < too homogeneous` expression to determine happiness but it was never stated (still working on this section I think). This does, however, seem like a valid route to explore. I'm also a little confused about the purpose of the different kernel sizes. While it does seem like an interesting variable to modify (and does seem to affect final segregation levels), I'm not sure what the real-world counterpart would be: what effect is this trying model? Overall both of these changes seem very doable and the team seems like they're on top of it and won't run into any major limitations.

## Results
**Do you understand what the results are (not yet considering their interpretation)?  If they are presented graphically, are the visualizations effective?  Do all figures have labels on the axes and captions?**

The current results are summed up in Figure 3.2. The graph seems to suggest that for almost any preference threshold, an increase in the kernel size will lower the segregation levels (except at the highest levels). I'm not sure if this the main takeaway the team wants from this graph. The graph needs a label for the y-axis and may benefit from actually having fewer coefficients displayed on the graph. It would be nice if the team added a bit that explained the significance of this graph and what the main takeaway is. It also might be good to extend the upper limit of the preference threshold to be more similar to the paper the figure is referencing; it might do a better job highlighting that the radius affects preference thresholds differently.

## Interpretation
**Does the draft report interpret the results as an answer to the motivating question?  Does the argument hold water?**

Currently the team has not implemented the heterogeneity part of the project so it's hard to determine how valid their interpretation is. It does seem like the team has acknowledged this and is planning on running several experiments to extract information from any characteristics the extension adds. 

## Replication
**Are the results in the report consistent with the results from the original paper?  If so, how did the authors demonstrate that consistency?  Is it quantitative or qualitative?**

Figure 3.2 looks to be consistent with the paper it is referencing. The team demonstrated this qualitatively by producing a graph that looked similar to Figure 5 in the supporting paper.

## Extension
**Does the report explain an extension to the original experiment clearly?  Can it answer an interesting question that the original experiment did not answer?**

It is clear what the extension is and what the purpose of the extension serves. Currently, it's not entirely clear how the team is going to implement this extension. I think it could be an interesting question. There's a chance the team finds a critical preference level where either side becomes very homogeneous or very mixed. It's hard to determine without seeing some models with the extension implemented but the team does seem to be aware of this and included it in their potential concerns. 

## Progress
**Is the team roughly where they should be at this point, with a replication that is substantially complete and an extension that is clearly defined and either complete or nearly so?**

The replication does seem to be complete but it might be worth writing a bit more about the effect of kernel sizes. As previously mentioned the extension needs work. 

## Presentation
**Is the report written in clear, concise, correct language?  Is it consistent with the audience and goals of the report?  Does it violate any of the recommendations in my style guidelines to an external site.?**

Overall the report is not too verbose which I really like. I think Figures 2.n should really be a plot with multiple subplots: they are also probably too large. I ctrl-F'd 5 of Allen's no-no words which seems kind of relatively reasonable. First person is used. Nothing is spelled wrong which is super impressive. 

## Mechanics
**Is the report in the right directory with the right file name?  Is it formatted professionally in Markdown?  Does it include a meaningful title and the full names of the authors?  Is the bibliography in an acceptable style?**

The repository looks good with the right folders and file names. The format is professional with a proper use of markdown. Both authors’ names are present and the title properly defines the goal of the paper without being too verbose. The bibliography is nice. The summary of each reference is probably not necessary but that's totally up to the authors' discretion.
