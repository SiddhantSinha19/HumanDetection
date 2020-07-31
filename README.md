Human Detection from a given image

I am really thankful to the deep learning community online for uploading various articles and their work.

For this project, I used transfer learning as training a model from scratch would have been extremely time consuming. I used Masked R-CNN model for this.

Dataset: Pascal VOC2005 challenge [I decided to go with this as it contained fewer images for human class (about 160 in total), which is sufficient for transfer learning.  Link - http://host.robots.ox.ac.uk/pascal/VOC/databases.html#VOC2005_1

Installing Mask R-CNN

git clone https://github.com/matterport/Mask_RCNN.git

cd Mask_RCNN

python setup.py install

Download the model weights here: https://github.com/matterport/Mask_RCNN/releases/download/v2.0/mask_rcnn_coco.h5


In order to run my project without making any changes make sure you have a following folder structure.

A main folder - called objectdetection

objectdetection/person/images/... [all the images goes here]

objectdetection/person/annots/... [all the annotation goes here (.txt)]

objectdetection/mask_rcnn_coco.h5  [weights of the pre-trained model]

objectdetection/Mask_RCNN/... [This will be created by git clone]

You are good to go now. Download "HumanDetection_mrcnn.ipynb" python notebook and save as in objectdetection/HumanDetection_mrcnn.ipynb 

Just run this notebook, it should train the model and then evaluate as well.

Please note that testingHumanDetection.ipynb is just evaluation of the model and will not work unless you have trained the model.

Explanation of code:

The function load_dataset() loads the dataset to a single class i.e. "person". The name of the images are person_001, person_002 and so on. So if the number is < 197, the number is loaded into the train set. And if the number is >= 197, then image is loaded into the test set. Finally the image is added to the dataset along with annotation path.

The function extract_boxes() extracts details of the image and bounding box from the annotations file. Annotations file is a text file. The dimensions of the image are always in 3rd line, so I extracted width and height from there. Further, after going through the annotations file, it can be seen that if a line has phrase "Bounding box", it will be followed be details of the box. So, I iterate through all the lines, and whenever the phrase is matched, box details are extracted. Note that there can be more than one bounding box in an image. [More than 1 person]

The next function load_mask() will load the mask for mrcnn. I will use our bounding boxes as our masks. So, this function simply calls the extract_boxes() functions from it and then creates masks from it.

Next, few cells of code is just to test the proper loading of train and test images.

PersonConfig() class defines the parameters for the model. Then the model is trained for 5 epoch after excluding the following layers "mrcnn_class_logits", "mrcnn_bbox_fc",  "mrcnn_bbox", "mrcnn_mask"

Evaluation of model

Model is evaluation by calculating IoU between predicted and actual bounding box. If IoU > 0.5, it is considered as a correct prediction. Then precision is found. And mAP is the mean average percision 

I get a mAP of 97.3 train set and 93.5 on test set.

Please note: Although I have an deep understanding of the code, convolution neural networks and MRCNN, I have taken help of the several articles and tutorials. As I already mentioned, I thank the deep learning community for contributing their work on open source platforms and via various articles/ tutorials. 

Also, a lot of people use annotations in the form of xml, I have used txt file here, because the dataset which I used is from 2005 and the annotations were provided in txt file. This should not be an issue if you are able to parse the text file and retrieve the required information from it.


If you have any query or issue - you can contact me at sid.ronaldo1904@gmail.com
