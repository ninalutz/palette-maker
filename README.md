# palette-extractor

Palette Extractor is an interactive web tool that allows you to explore different approaches to extract color palettes from images.

# Features 
When the app starts, you simply browse and select a local image. The app then loads the image and plots in in three dimensional RGB space.

![](https://cloud.githubusercontent.com/assets/4796480/20862220/18261e3e-b973-11e6-9f47-834f08442274.png)

## Palette Extraction Algorithms
Three different palette extraction algorithms are currently supported.

### Simple Histogram Binning
The histogram binning approach partitions the RGB space into a NxNxN grid where N is a user provided value. The below image shows an example when `N=3`. Here, the space is partitioned into 27 equally sized cells. The pixels that fall within each cell are counted, and their average color value is computed. Average colors from the most populated 10 cells are selected and displayed as the color palette.

<div>
<img src="https://cloud.githubusercontent.com/assets/4796480/20862225/2320124a-b973-11e6-9855-112a11482a57.png" width="460">
<img src="https://cloud.githubusercontent.com/assets/4796480/20862228/3687934e-b973-11e6-87cf-cf4915e511c8.jpg" width="400">
</div>

### Median Cut Space Partitioning
[Median cut](https://en.wikipedia.org/wiki/Median_cut) also partitions the space, though it does to in a non-uniform way. The pixel range is computed for each color dimension (red, green, and blue). Then, the dimention with the largest range is selected, and the median value is computed. The space is then split into two halves - one above the median, and one below. This process continues recursively. Each iteration, only the subspace with greatest pixel range is split. A sample partitioning looks like this:

<div>
<img src="https://cloud.githubusercontent.com/assets/4796480/20862222/1d3c5276-b973-11e6-8260-7a177b363292.png" width="460">
<img src="https://cloud.githubusercontent.com/assets/4796480/20862231/401d685c-b973-11e6-8a7c-f752ac0a77cd.jpg" width="400">
</div>

### K-Means Clustering
[K-Means](https://en.wikipedia.org/wiki/K-means_clustering) attempts to cluster the pixels into k distinct clusters. The user provides a k value as input.

Since k-means is notorious for getting stuck in local minima, the algorithm is re-run 100 times and the result with lowest error is selected. An example output from running k-means on the above image is shown below.

<div>
<img src="https://cloud.githubusercontent.com/assets/4796480/20862226/29f32ab2-b973-11e6-9690-51d714f7847e.png" width="460">
<img src="https://cloud.githubusercontent.com/assets/4796480/20862229/395f0728-b973-11e6-982b-e99b2c211b10.jpg" width="400">
</div>

# Development
To run the project, clone the repository, then run

```
npm install
```

The javascript can be built via

```
webpack
```

This will generate a single `bundle.js` file, containing all of the javascript.