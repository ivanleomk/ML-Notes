 The intuition behind PCA is that we'd like to try and represent high dimensional vectors in a 2 or 3 dimensional space so that we can visualise our data distribution.

We typically do this by maximising the sum of the squared distances along a random line along the origin when comparing two different potential features. By finding this best fit line, we can combine the two features into a single Principal Component as seen below.

![](assets/CleanShot%202024-06-17%20at%2009.47.36.png)

In other words, the new Principal Component is a linear combination of two or more previous features. We then have a few other specialised terms such as

- **Eigenvalue** : The SS(distances) / n-1 
- **Singular Value** : Square Root of the SS(distances)

