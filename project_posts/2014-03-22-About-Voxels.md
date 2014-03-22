## What is a Voxel?

The subject`s brain activity in this image is sending signals to the fMRI related to the task.The red specks that stand out the background is showing where blood is flowing in the brain. fMRI images represents these activities according to changes in blood oxygen level, a proxy for degree of mental activity.

It`s important to understand what fMRI pictures actually show.

Our brain like the rest of our body relies on oxygen. Parts of the brain the uses more energy is taxing more oxygen. Our body is filled with hydrogen atoms, each one a single proton with an electron orbiting it. Protons present in the blood behaves or vibrates differently when it contains more oxygen. The fMRI takes advantage of this ratio of blood with oxygen and the blood without. This ratio is called as the BOLD, or blood oxygenation-level dependent signal, and use it to calculate parts of the brain that are most active in a given time. fMRI is not very fast in capturing all of the changes in the brain. Each scan requires a second or two, which is enough time for a neuron to fire more than a hundred times. 

fMRI also does not represent the detail level of a cell.The 3D image it provides is built up in units called voxels which shows the brain tissue as a cube or block.  Each voxel can represent a million of brain cells. This 3D image block is synonymous to the pixels in the computers graphical screens, albeit in 2D. The red specks in the brain scan are actually clusters hundreds of voxels.

The brain is complex and involves multiple processes, a careful deduction is a must. For instance, each time a person sees a snake, and lights up to a specific area of the brain, we cannot deduce that its the same area that lights up when the person is afraid. 

However, through careful statistics, it´s possible to identify significant activity by comparing changes within each individual voxel when for instance the person is idle or not doing anything, and when it doing a specific task. fMRI is a a great tool to show correlations, say, when you are watching a movie, fMRI can point us the associated activity in clusters of neighboring voxels which correspond to an a particular brain region say, visual cortex. 


#### So, how can we use these voxel to come up with a mapping machine as what Gallant Lab calls brain-reading ? 

1. We need to model how clusters of activity in the brain`s voxels corresponds to what a subject is seeing. This gives us a semantic map of words and events and the corresponding areas of brain activation.

What Gallant Lab does is to ask subjects to watch hours of movies while inside an fMRI. The visual stimuli is then mapped out the to the pattern of voxel activation. For each of say, 50,000 voxels in the brain, brain researchers create several models to generate a comprehensive description of what is actually happening in the subject`s brain. 

2. Using the model generated in the first step, the calculated fMRI data correlations can be used to help a machine/program to decode what the subject is seeing. Another research activity made by Gallant Lab is reversing the process and decoding brain activity to recreate a video that predicts what the subject is actually seeing (see, http://www.youtube.com/watch?v=nsjDnYxJ0bo)





![fMRI Scan](../project_images/FMRI_scan_during_working_memory_tasks.jpg?raw=true "fMRI Scan")

Credit: http://www.frontiersin.org/Neurotrauma/10.3389/fneur.2013.00016/full, Via: Wikimedia Commons


Peak BOLD responses to each of the 1,750 training and 120 validation images were estimated
from the preprocessed data. Gallant Lab provide these estimated responses in their file. The file is stored in matlab version 7.3 .mat file format, which is equivalent to hf5 format, and can be read directly into numpy/python using the PyTables library.



![fMRI V1 Voxels](../project_images/Gallant_data_python.png?raw=true "fMRI V1 Voxels")


The responses for each voxel have been z-scored, so for a given voxel the units of each
"response" are standard deviations from that voxel's mean response. Also, of the 73,728
(64X64X18) voxels recorded for each scan, only ~25,000 voxels in or near the cortex were
selected for each subject. ROIs for each subject were determined based on separate localizer
scans (not included). See Kay et al (2008) for details of BOLD response estimation, voxel
selection, and ROI definition.

The following code is how we loaded the code into python 
# To get all V1 voxel responses in the training data set:

´´´
import tables,numpy
f = tables.openFile('EstimatedResponses.mat')
f.listNodes # Show all variables available
Dat = f.getNode('/dataTrnS1')[:]
ROI = f.getNode('/roiS1')[:].flatten()
V1idx = numpy.nonzero(ROI==1)[0]
V1resp = Dat[:,V1idx]
print V1resp
´´´

![fMRI V1 Voxels](../project_images/Gallant_data_print_V1_voxels.png?raw=true "fMRI V1 Voxels")


-- References --
Kay, K. N., Naselaris, T., Prenger, R. J., & Gallant, J. L. (2008). Identifying natural images
from human brain activity. Nature, 452(7185), 352-355.

Naselaris, T., Prenger, R. J., Kay, K. N., Oliver, M., & Gallant, J. L. (2009). Bayesian
reconstruction of natural images from human brain activity. Neuron, 63(6), 902-915.

