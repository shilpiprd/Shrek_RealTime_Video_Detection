### Unconventional Changes 
- Had to change line#82 in train.py, since we're using train/test in our case and not train/valid as is specified in the data/customdata/custom.txt file. 
- Had to add ``ns = int(...) `` as this was a typo before. 
- Changed valid to 'test' in smalcoco.data file.
- Changed valid to test in test.py in root folder 

### Final Video Inferencing 
- To get the final output, I intend to run a combination of 2 commands. 
- 1st command is : !python detect.py --conf-thres 0.1 --output out_out (this is assumign that test and train images are in same folder ) 
- 2nd command is : !python detect.py --weights path_to_your_trained_weights   
- After my model is done training, i should apparently have some weights inside the weights folder in the end like last.pt. 

