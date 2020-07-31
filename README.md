Human Detection from a given image

I am really thankful to the deep learning community online for uploading various articles and their work.

For this project, I used transfer learning as training a model from scratch would have been extremely time consuming. I used Masked R-CNN model for this.

Dataset: Pascal VOC2005 challenge [I decided to go with this as it contained fewer images for human class (about 160 in total), which is sufficient for transfer learning. 

Installing Mask R-CNN

git clone https://github.com/matterport/Mask_RCNN.git

cd Mask_RCNN
python setup.py install
Download the model weights here: 


In order to run my project without making any changes make sure you have a following folder structure.

A main folder - called objectdetection

objectdetection/person/images/... [all the images goes here]

objectdetection/person/annots/... [all the annotation goes here (.txt)]

objectdetection/mask_rcnn_coco.h5  [weights of the pre-trained model]

objectdetection/Mask_RCNN/... [This will be created by git clone]

You are good to go now. Download "HumanDetection_mrcnn.ipynb" python notebook and save as in objectdetection/HumanDetection_mrcnn.ipynb 

Just run this notebook, it should train the model and then evaluate as well.

If you want to just evaluate the model without any training, simply donwload "person_model20200731T0029" folder from this repository. This has saved model after training, and has 5 different files. Each file is model's data after one epoch. Save this folder in objectdetection folder as objectdetection/person_model20200731T0029

Then download testingHumanDetection.ipynb and run it. It should evaluate the model.
