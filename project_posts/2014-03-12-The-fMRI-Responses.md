## The fMRI BOLD responses data

Our training data containing the fMRI BOLD responses to natural imagery was from the Collaborative Research in Computational Neuroscience (CRCN.org) or Gallant.org. Unfortunately, only people with University affiliation are able to request data from them (But if your intentions are noble, send an email). Gallant Labs training data contains 1,750 responses (one per training image) in each of ~25,000 voxels and the validation data is 120 responses in each of ~25,000 voxels. If you don`t have a Matlab software you can access the data using python (you'll need the pyTables library and numpy).

Below is a sketch studying how we can use the data from UC Berkeley in Dreamsprawler:



![fMRI BOLD Responses](../project_images/Data_UCBerkeley.png?raw=true "fMRI BOLD Responses")



In the Gallant Lab`s research, they are showing that the brain organises concepts along a continuous map. A huge range of categories are organised according to different features, for instance if the object is biological or artificial or whether they are moving or still. Areas that represent similar concepts animals and humans or houses and buildings —tend to be close together, while most disparate categories are farther apart. These patterns are consistent across different individuals. They also mentioned that this arrangement is an efficient one because it takes a lot of energy for the neurons in the brain to communicate with one another, especially if they have long connections between them. “One can assume that the brain is trying to minimise the length of the wires...One way of doing that is to put bits that are doing similar computations next to each other (J. Gallant).”



**References in Brain-Reading**

[![ScreenShot1](../project_images/ref_5.png?raw=true)](http://www.youtube.com/watch?v=u9nMfaWqkVE)
[![ScreenShot2](../project_images/ref_6.png?raw=true)](http://cdn.theguardian.tv/mainwebsite/2013/10/23/131023BrainDecoding-16x9.mp4)


**Other References**

Kay, K. N., Naselaris, T., Prenger, R. J., & Gallant, J. L. (2008). Identifying natural images from human brain activity. Nature, 452(7185), 352-355.

Huth, Nishimoto, Vu & Gallant. (2012). A Continuous Semantic Space Describes the Representation of Thousands of Object and Action Categories across the Human Brain. Neuron http://dx.doi.org/10.1016/j.neuron.2012.10.014

