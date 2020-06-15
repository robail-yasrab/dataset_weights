# Calculating Weights of Dataset Classes 
When you are trying to segment different classes from a given dataset and areas of interest are difficult to segment. There is a way you can calculate the weights of each class in given dataset's ground truth (mask). These weights could be used during the training process to help CNN to better segment. 

## How to use 
You are using the PyTorch Cross-Entropy Loss function. Here is the way to use given weights: 

### Download and Run 
Download and edit for your ground truth (mask) directory.
```
git clone https://github.com/robail-yasrab/dataset_weights.git
cd dataset_weights
python weight.py     #change input address to your ground truth directory 
```
### Code for Training 
add these weights in your training code. 
```
weights =[0.0007,0.7218,1.7989,0.0939,1.6279,7.3893]    #sample weights for 6 classes. 
class_weights = torch.FloatTensor(weights).cuda()       # add or remove cuda() in case of GPU availability
```
### Loss Function  
Change Cross Entropy Loss function definition: 

'''
loss = torch.nn.CrossEntropyLoss(weight=class_weights)
'''






## Reference from RootNav 2.0 
It is common in root images that the number of background pixels heavily outweigh the foreground. Calculating a loss over an unbalanced dataset such as this is likely to cause a bias towards background pixels, causing error and undersegmentation of the foreground. We apply a class-balancing approach to the standard cross-entropy loss, based on median frequency balancing. Weights are assigned to each class inversely proportional to the median frequency in which that class appears throughout the entire training set. This reduces the weight for classes that appear more often, in this case background, and increases the weight of foreground classes such as first-order roots [[1]](#1). 



## References
<a id="1">[1]</a> 
Yasrab, R., Atkinson, J. A., Wells, D. M., French, A. P., Pridmore, T. P., & Pound, M. P. (2019), 
RootNav 2.0: Deep learning for automatic navigation of complex plant root architectures, 
GigaScience, 8(11), giz123.

