t-SNE gives you a feel and intuition on how data is arranged in higher dimensions. It is often used to visualise complex datasets into two and three dimensions, allowing us to understand more about underlying patterns and relationships in the data.

It's an alternative to [[Principal Component Analysis]] and helps us to generate and find clusters.

> Main question : What is the probability that a point chooses another point at random as it's neighbour

The benefit of using t-SNE is that it works on a pair-wise basis and aims to preserve the relationship between two pairs of data. The high level overview is that we 

1. Visualise the distance between two points proportional to the distance between the two points using a gaussian distribution
2. 