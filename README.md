# Task
YoloV3 Simplified for training on Colab with custom dataset. 
This project introduces a real-time object detection model specifically trained to recognize characters from the movie "Shrek." Utilizing advanced deep learning techniques, the model can accurately detect and draw bounding boxes around the identified characters in any given video frame. Along with visual identification, the model also quantifies its confidence level by indicating the probability of the detected object truly belonging to one of the trained classes.

The primary objective of this project was to demonstrate the capability of training an object detection system on a custom dataset, thereby highlighting its versatility and adaptability to varied use-cases. In this case, the model was trained on four distinct classes, representing characters from the movie.

I have used 110 images as training_set out of which for each class, there is roughly 25 images.
The corresponding label file (.txt file) of images contains the class_id and the bounding box coordinates.
The training and test images have been resized to the standard input size of YoloV3 by using Pillow. 

You'll need to download the weights from the original source. 
To be able to run the colab notebook, follow the given steps:
1. Create a folder called weights in the root folder.
2. Download from: https://drive.google.com/file/d/1vRDkpAiNdqHORTUImkrpD7kK_DkCcMus/view?usp=share_link
3. Place 'yolov3-spp-ultralytics.pt' file in the weights folder:
  * to save time, move the file from the above link to your GDrive
  * then drag and drop from your GDrive opened in Colab to weights folder
4. run this command
!python train.py --data data/customdata/custom.data --batch 10 --cache --cfg cfg/yolov3-custom.cfg --epochs 300 --nosave

The hierarchy of the data file is as follows:
```
data
  --customdata
    --train_images/
      --img001.png
      --img002.png
      --...
    --train_labels/
      --img001.txt
      --img002.txt
      --...
    custom.data #data file
    custom.names #contains the class name
    custom.txt #list of names of the train & test images that our model will be trained & tested on.
```

### Final Video Inferencing 
- To get the final output, I intend to run the following command ``!python detect.py --source /content/drive/MyDrive/Shrek_YOLOv3/frames_source --output out_out --conf-thres 0.1 ``
- After the model is done training, we would have the last.pt file inside the weights folder and the final output images inside the out_out folder. 

### Unconventional Changes 
- Had to change line#82 in train.py, since we're using train/test in our case and not train/valid as is specified in the data/customdata/custom.txt file. 
- Had to add ``ns = int(...) `` as this was a typo before. 
- Changed valid to 'test' in smalcoco.data file.
- Changed valid to test in test.py in root folder 
- I couldn't use gpu training before, because one of the tensor was not being converted to gpu. So I added this line in utils/utils.py file : a = a.to('cuda:0') .I had to hardcode it, but Now gpu training works.