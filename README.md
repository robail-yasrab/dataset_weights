# dataset_weights

It is common in root images that the number of background pixels heavily outweigh the foreground. Calculating a loss over an unbalanced dataset such as this is likely to cause a bias towards background pixels, causing error and undersegmentation of the foreground. We apply a class-balancing approach to the standard cross-entropy loss, based on median frequency balancing. Weights are assigned to each class inversely proportional to the median frequency in which that class appears throughout the entire training set. This reduces the weight for classes that appear more often, in this case background, and increases the weight of foreground classes such as first-order roots [[1]](#1). 








## References
<a id="1">[1]</a> 
RootNav 2.0: Deep learning for automatic navigation of complex plant root architectures, Yasrab et al. (2019). 
GigaScience, Volume 8, Issue 11, November 2019.
