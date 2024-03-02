# How to Run
<TABLE>
  <colgroup>
       <col span="1" width='300px'>
       <col span="1">
  </colgroup>
  
  <TR>
    <TH width='300px'>Folder Structure</TH>
    <TH>Folder Description</TH>
  </TR>
  
<TR>
  <TD>
    <div>
      <IMG src='https://github.com/KeeBoonHwee/ASTAR_NMC_IWSP/assets/97490747/f711eb6c-779d-4ac1-a887-e9c2994e4326' width='300px' />
    </div>
  </TD>
  <TD>
  <div>Please run GanNarrate.cmd.</div><BR>
  </TD>
</TR>

<TR>
  <TD>
    <div>
      <IMG src='https://github.com/KeeBoonHwee/ASTAR_NMC_IWSP/assets/97490747/eeafa090-0a2a-40a4-8960-85cd4d616669' width='300px' />
    </div>
  </TD>
  <TD>
    <div> You will be prompted to select .csv input file. Please choose the file "SubjectImage.csv".
  </TD>
</TR>

<TR>
  <TD>
    <div>
      <IMG src='https://github.com/KeeBoonHwee/ASTAR_NMC_IWSP/assets/97490747/eeafa090-0a2a-40a4-8960-85cd4d616669' width='300px' />
    </div>
  </TD>
  <TD>
    <div> You will be prompted to select .csv input file subject. Please choose the corresponding number tied to the subject image that you wish GAN-Narrate to evaluate.
  </TD>
</TR>

<TR>
  <TD>
    <div>
      <IMG src='https://github.com/KeeBoonHwee/ASTAR_NMC_IWSP/assets/97490747/eeafa090-0a2a-40a4-8960-85cd4d616669' width='300px' />
    </div>
  </TD>
  <TD>
    <div> You will be prompted to select the CNN Model. Please choose the CNNModel.pkl file.
  </TD>
</TR>

</TABLE>
<HR>
</BODY>
</HTML>

# GAN-Narrate: Enhancing Image Repair with Enumerating Layers in a Supervised-Unsupervised Ensemble Model
While OCR/ICR has made significant advancements and becoming more prolific such as in the use of translational services, office digitisation  and license plate recognition, OCR/ICR technologies still face many challenges and limitations. It has been reported that OCR/ICR accuracy tends to decrease with complex fonts, decorative typography, and non-standard layouts. Neumann’s and Matas’ research into the use of OCR/ICR found that perspective effects, diverse fonts and languages, differing alignment of real-world text added challenges. Generative neural networks are a class of neural networks used in machine learning that learns to generate new data resembling the original dataset it was trained on. Examples can be images, sounds, or text, that mimic the characteristics of the training data. The GAN framework introduced by Ian Goodfellow and his peers in 2014 is often credited as a breakthrough in the field of GAN. 

- (J.-H. Kuo, C.-M. Huang, W.-H. Liao, and C.-C. Huang, HuayuNavi: A Mobile Chinese Learning Application Based on Intelligent Character Recognition, in Edutainment Technologies. Educational Games and Virtual Reality/Augmented Reality Applications , Sep. 2011, pp. 346–354. doi: 10.1007/978-3-642-23456-9_63)
- (D. Dipti, N. N. R. R. Suri, and A. R, Preprocessing and Image Enhancement Algorithms for a Form-based Intelligent Character Recognition System, International Journal of Computer Science & Applications, vol. 2, no. 2, pp. 131–144, 2005)
- (Z. Jian, X. Fan, and H. Cailun, Research on Characters Segmentation and Characters Recognition in Intelligent License Plate Recognition System, in Chinese Control Conference, IEEE, Aug. 2006, pp. 1753–1755. doi: 10.1109/CHICC.2006.280847)
- (L. Neumann and J. Matas, A Method for Text Localization and Recognition in Real-World Images, Lecture Notes in Computer Science , Nov. 2010, pp. 770–783. doi: 10.1007/978-3-642-19318-7_60)

## GAN-Narrate
This effort focuses on the viability of using a modified GAN framework to generate features that can be used to address the challenges faced by OCR/ICR, repairing ‘broken’ or ‘damaged’ data. 
1) A CNN (Convolutional Neural Network) model will be used to assess an Input Image X, returning the predicted class label of the image as well as of the confidence of the prediction.
2) A modified GAN dubbed Feature GAN will be used to generate a feature to repair Input Image X based on the predicted class label from CNN. This feature is called Feature Z.
3) Feature Z will be combined with Input Image X, and result in Combined Image Y. The CNN model will be called again to assess Combined Image Y, returning the predicted class label of the image as well as of the confidence of the prediction. 

## Principle 
An active learning approach is utilised in GAN-Narrate with Input Image X being used as a constant reinforcement learning guide during the iterative gradient descent of Feature GAN’s backpropagation. This considers that Feature GAN comprising of two neural network models: the Feature Generator Model and the Discriminator Model, related through: 

![Capture](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/964f867e-570f-4c65-9f99-5796fbfe2007)

Where G(z) refers to the Feature Generator Model creating an output (that we can designate x_feature) onto a random input latent vector, z. D(x) refers to the Discriminator Model that receives an input (x_feature or x_truth) and attempts to discriminate between 2 conditions: x_feature or x_truth outputting a binary discrete condition of TRUE or FALSE. This method approaches continuously inserting of an enumerating layer reflecting Input Image X appended onto the x_feature, manipulating the Discriminator model losses to accrue through a criterion whenever it fails to account for the modified x_feature. 

## Convolutional Neural Network
A computer vision-abled CNN will be trained with the MNIST dataset for all labels (42,000 examples). In this experiment, the CNN is based upon the Numpy-CNN code designed by Alescontrela that is available and was taken from GitHub (https://github.com/Alescontrela/Numpy-CNN).

![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/23f69ca9-2e21-4103-a414-41dcd7aa40a0)

![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/c4c55be5-4356-4d26-952e-9f8f22df1a8e)

## Feature GAN Model
A single untrained Feature GAN framework that will be actively trained with the MNIST dataset (60,000 examples) during the duration of Feature GAN is deployed. This single untrained Feature GAN framework will be used for all MNIST class labels introduced into GAN-Narrate. 

### Feature Generator Model
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/89f383a7-07f4-478e-9095-4049132de115)

![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/d2125311-8e92-4642-b5c2-b3345d7e4a89)

### Discriminator Model
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/5aa37f58-dc35-4153-bf9c-6aaad9051cd5)

![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/0f3b2583-ee42-41aa-bba0-4a9ebb34bcf7)

## Experimentation Results
The following types of handwritten damages are assessed: ‘dashed-across’ damage, smudging damage, speckled damage and noise damage. In each type of potential damage, the following testing conditions are considered: 
- 100 examples of each potential damage are analysed.
- Success case: If the class label initially identified by the CNN is the same as after GAN-Narrate has been called to repair the image, as well as there being an increase of confidence after GAN-Narrate’s activity.
- Failure case: If the class label initially identified by the CNN is different from after GAN-Narrate has been called to repair the image, or there is a decrease of confidence after GAN-Narrate’s activity.

All experimentations were performed with the following hardware considerations: A NVIDIA GeForce RTX 2080 Ti was utilised that ran on-site at University of Newcastle upon Tyne located in Singapore within the Singapore Institute of Technology @ Nanyang Polytechnic. This is configured with CUDA Cores: 2944, Tensor Cores: 368, Base Clock: ~1515 MHz, Boost Clock: ~1710 MHz, Memory: 8GB GDDR6, Memory Speed: 14 Gbps, Memory Bus: 256-bit and Memory Bandwidth: 448 GB/s. 

- Processor: Intel(R) Xeon(R) CPU E5-1607 v4 @ 3.10GHz
- Installed RAM: 64.0 GB
- Display Adapter: NVIDIA GeForce RTX 2080 Ti
- System: Windows 10 Pro. 64-bit operating system, x64-based processor
- Version: 22H2
- OS build: 19045.3693
- Experience: Windows Feature Experience Pack 1000.19053.1000.0
- CUDA build: 11.2.r11.2/compiler.29373293_0
- CUDA DNN build: 8.1.1

## Testing of ‘Dashed Across’-Type Damage
This occurs when there is a thin smudge that removes features from an existing handwritten digit and runs a significant length of the digit.

### ‘Dashed Across’-type damage repaired with GAN-Narrate: Input Image X with ‘dashed across’-type damage
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/d177d2dd-3d8c-4801-99eb-f892f3f634b2)

### ‘Dashed Across’-type damage repaired with GAN-Narrate: Combined Image Y, after being repaired by GAN-Narrate
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/5172c95c-86c2-4c9c-af2b-5cad3f2e4eb1)

### Success and Failure cases for GAN-Narrate’s ability to repair ‘dashed across’-type damage in 100 examples
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/566a6bb6-c317-4ff4-9927-1778e751c321)

## Testing of Speckled-Type Damage
This occurs when there is a loss of features not necessarily confined to a particular area of the image but throughout the handwritten subject.

### Speckled-type damage repaired with GAN-Narrate: Input Image X with speckled-type damage
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/10498e81-93f1-41a3-bc70-c9762b99ab0e)

### Speckled-type damage repaired with GAN-Narrate: Combined Image Y, after being repaired by GAN-Narrate
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/3b365a99-2d9a-49d1-881a-a0e53685172a)

### Success and Failure cases for GAN-Narrate’s ability to repair speckled-type damage in 100 examples
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/99242fdd-5ed7-4a5c-96c9-100c75297a7e)

## Testing of Smudging-Type Damage
This refers to a loss of features from the existing handwritten digit being significant in terms of width

### Smudging-type damage repaired with GAN-Narrate: Input Image X with smudging-type damage 
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/47962488-5750-4074-99f1-2a9392ee455c)

### Smudging-type damage repaired with GAN-Narrate: Combined Image Y, after being repaired by GAN-Narrate
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/b8a0f978-7f80-4bf2-b16a-a393eddbf063)

### Success and Failure cases for GAN-Narrate’s ability to repair smudging-type damage in 100 examples
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/b600b4bd-e947-4155-b617-a8d80b8bd885)

## Testing of Noise-Type Damage
This occurs when there are additional handwritten features (noise) that adversely affects and do not contribute to the discernability of the handwritten digit.

### Noise-type damage repaired with GAN-Narrate: Input Image X with noise-type damage
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/6cd16405-06ea-4697-80bd-79ed9040f5c7)

### Noise-type damage repaired with GAN-Narrate: Combined Image Y, after being repaired by GAN-Narrate
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/395e1612-ae9a-4ea8-b8d8-22d9da3b5395)

### Success and Failure cases for GAN-Narrate’s ability to repair noise-type damage in 100 examples
![image](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/da8b55e2-493f-46df-a506-f8563bdd8246)

## Results and Findings
GAN-Narrate is able to perform in the capacity of detection, assessment, generation of repair features, usage of features to repair the subject image and re-assessment of the subject image. A result of the experiments found that with the current holding parameters, 10-20 epochs were generally sufficient for GAN-Narrate’s Feature Generator Model and Discriminator Model to reach a point of convergence in their loss functions to generate a viable repair feature. 
GAN-Narrate proves successfully in being able to cater to a wide range of damages that might afflict certain handwritten applications, finding success in ‘dashed across’-type damage, smudging-type damage and speckled-type damage. However, GAN-Narrate proves to have difficulty in noise-type damage. 
