## What are Voxels, fMRI, BOLD responses and all these jargons?

The subject`s brain activity in the image shown below is sending signals to the fMRI related to the task. The red specks that stand out in the background is showing where blood is flowing in the brain. fMRI images represents these activities according to changes in blood oxygen level, a proxy for degree of mental activity. It is important to understand what fMRI images actually show for us to create an object to brain location mapping in our project.

Our brain like the rest of our body relies on oxygen. Parts of the brain the uses more energy is taxing more oxygen. Our body is also filled with hydrogen atoms, each one a single proton with an electron rotating it. Protons that are present in the blood behaves or vibrates differently when it contains more oxygen. fMRI takes advantage of this ratio of blood with oxygen and blood without. This ratio is called as the BOLD, or blood oxygenation-level dependent signal, and we can use it to calculate parts of the brain that are most active in a given time. fMRI is not very fast in capturing all of the changes in the brain. Each scan requires a second or two, which is enough time for a neuron to fire more than a hundred times. 

fMRI also does not represent the detail level of a cell. The 3D image of an fMRI is built up in units called voxels which shows the brain tissue as a cube or block.  Each voxel can represent a million of brain cells. This 3D image block is synonymous to the pixels in the computers graphical screens, albeit in 2D. The red specks in the brain scan image shown below are actually clusters hundreds of voxels.

The brain is complex and involves multiple processes, a careful deduction is a must. For instance, each time a person sees a snake, and lights up to a specific area of the brain, we cannot deduce that its the same area that lights up when the person is afraid. However, through careful statistics, it is possible to identify significant activity by comparing changes within each individual voxel when for instance the person is idle or not doing anything, and when doing a specific task. fMRI is a a great tool to show correlations, say, when you are watching a movie, fMRI can point us the associated activity in clusters of neighboring voxels which correspond to a particular brain region say, visual cortex. 


![fMRI Scan](../project_images/FMRI_scan_during_working_memory_tasks.jpg?raw=true "fMRI Scan")

Image credit: http://www.frontiersin.org/Neurotrauma/10.3389/fneur.2013.00016/full, via: Wikimedia Commons


**So, how can we use these voxels to come up with a mapping machine as what Gallant Lab calls brain-reading?** 


[1]  We need to model how clusters of activity in the brain`s voxels corresponds to what a subject is seeing. This gives us a semantic map of words or objects and the corresponding areas of brain activation.

What Gallant Lab did was to ask subjects to watch hours of movies while inside an fMRI. The visual stimuli is then mapped out with the pattern of voxel activation. For each, say, 50,000 voxels in the brain, researchers create several statistical models to generate a comprehensive description of what is actually happening in the subject`s brain. 

[2]  Using the model generated in the first step, the calculated fMRI data correlations can be used to help a machine/program decode what the subject is seeing. This process leads to another research activity made by Gallant Lab where they are reversing the process and decoding brain activity to generate a video that shows prediction of what the subject is actually seeing (see, http://www.youtube.com/watch?v=nsjDnYxJ0bo)

Peak BOLD responses to each of the 1,750 training and 120 validation images were estimated from the preprocessed data. Gallant Lab provide these estimated responses in their file. The file is stored in a .mat file format, which is equivalent to hf5 format, and can be read directly using the PyTables library in python. The responses for each voxel have been z-scored, so for a given voxel the units of each "response" are standard deviations from that voxel's mean response. Also, of the 73,728 (64X64X18) voxels recorded for each scan, only ~25,000 voxels in or near the cortex were selected for each subject. ROIs for each subject were determined based on separate localizer scans (not included). See Kay et al (2008) for more details of BOLD response estimation, voxel selection, and ROI definition.


The following code is how we loaded the data into python to get all voxel responses in the human primary visual cortex (V1) in the training data set:

```
import tables, numpy
f = tables.openFile('EstimatedResponses.mat')
f.listNodes # Show all variables available
Dat = f.getNode('/dataTrnS1')[:]
ROI = f.getNode('/roiS1')[:].flatten()
V1idx = numpy.nonzero(ROI==1)[0]
V1resp = Dat[:,V1idx]
print V1resp
```

Using the `f.listNodes` shows all variables available in the file:

- dataTrn (S1/S2) : 1,750 x ~25,000 matrix; 1,750 responses (one per training image) in each
of ~25,000 voxels
- dataVal (S1/S2) : 120 x ~25,000 matrix; 120 responses in each of ~25,000 voxels
- voxIdx (S1/S2) : index for mapping the ~25,000 voxels into a 64 x 64 x 18 volume.
- roi (S1/S1) : indices for which voxels correspond to each ROI.


![fMRI V1 Voxels](../project_images/Gallant_data_python.png?raw=true "fMRI V1 Voxels")

The result is a large dataset with thousands of voxel responses:

![fMRI V1 Voxels](../project_images/Gallant_data_print_V1_voxels.png?raw=true "fMRI V1 Voxels")


Kay et al. (2008) used receptive-field models to build a visual decoder from fMRI data. In the algorithm training step, they established how the activity of each voxel in the visual cortex responded to locations, orientations and spatial frequencies presented in 1750 images. In the image identification step, they presented images out of a set which was not used during the training session. By measuring the response of each voxel to the new image, and comparing it with the predicted response for each image out of this new set, they were able to guess which image was actually seen by the subject. Out of over a thousand of images (for example, apple 1, apple 2,... cat 1, cat 2, cat 3,...etc.), fMRI can predict which image the subject is actually seeing (for example, cat 1). 

**References**

Kay, K. N., Naselaris, T., Prenger, R. J., & Gallant, J. L. (2008). Identifying natural images
from human brain activity. Nature, 452(7185), 352-355.

Naselaris, T., Prenger, R. J., Kay, K. N., Oliver, M., & Gallant, J. L. (2009). Bayesian
reconstruction of natural images from human brain activity. Neuron, 63(6), 902-915.

Huth, Nishimoto, Vu & Gallant. (2012). A Continuous Semantic Space Describes the Representation of Thousands of Object and Action Categories across the Human Brain. Neuron http://dx.doi.org/10.1016/j.neuron.2012.10.014

