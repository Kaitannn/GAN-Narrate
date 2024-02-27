# GAN-Narrate: Enhancing Image Repair with Enumerating Layers in a Supervised-Unsupervised Ensemble Model
While OCR/ICR has made significant advancements and becoming more prolific such as in the use of translational services , office digitisation  and license plate recognition , OCR/ICR technologies still face many challenges and limitations. It has been reported that OCR/ICR accuracy tends to decrease with complex fonts, decorative typography, and non-standard layouts . Neumann’s and Matas’ research into the use of OCR/ICR found that perspective effects, diverse fonts and languages, differing alignment of real-world text added challenges. Generative neural networks are a class of neural networks used in machine learning that learns to generate new data resembling the original dataset it was trained on. Examples can be images, sounds, or text, that mimic the characteristics of the training data. The GAN framework introduced by Ian Goodfellow and his peers in 2014 is often credited as a breakthrough in the field of GAN. 

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
An active learning approach is utilised in GAN-narrate with Input Image X being used as a constant reinforcement learning guide during the iterative gradient descent of Feature GAN’s backpropagation. This considers that Feature GAN comprising of two neural network models: the Feature Generator Model and the Discriminator Model, related through: 

![Capture](https://github.com/Kaitan1995/GAN-Narrate/assets/93040738/964f867e-570f-4c65-9f99-5796fbfe2007)

Where G(z) refers to the Feature Generator Model creating an output (that we can designate x_feature) onto a random input latent vector, z. D(x) refers to the Discriminator Model that receives an input (x_feature or x_truth) and attempts to discriminate between 2 conditions: x_feature or x_truth outputting a binary discrete condition of TRUE or FALSE. This paper approaches continuously inserting of an enumerating layer reflecting Input Image X appended onto the x_feature, manipulating the Discriminator model losses to accrue through a criterion whenever it fails to account for the modified x_feature. 
