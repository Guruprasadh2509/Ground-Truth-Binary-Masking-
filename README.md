### Binary Mask File Generation (Generating Ground truth images)

There are two files placed here. 

One is custom_1.py, this contains the class and functions defined for generating the ground truth image.

Another one is JSON_TO_MASK_V1.ipynb, on executing this ipynb, the binary ground truth is generated.

I tried below approach for generating binary masking (ground truth):

Below are the steps which made me to get my goal achieved , that is creation of ground truth images.

Steps:

1.create a folder called train  place the images for whom , ground truth needs to be generated
  create another folder called train_masked.
  
2.Using VIA tool, annotate the objects(using Polygon drawing method),(I tried with VIA 1.0.6), save the json file(via_region_data.json) 
  and place generated json inside the created folder "train", where the images are placed for generating ground truth images.
  
3.Install mrcnn library(!pip install mrcnn)

4.In custom_1.py, following changes need to be updated.

  1.Update the root directory path in 12th line, where train folder is created.
  
  2.In CustomConfig class:  


    a.In 28th line across NAME variable, replace the "annotated label" with your annotated label, which was created using VIA tool.
    
    b.In 34th line update NUM_CLASSES (1-Background, 1-foreground)(binary object masking)
    
  3.In CustomDataset class:
  
    a.In load_custom function, 48th line replace the "annotated label" with your annotated label.
        
    b.in 91st line under "self.add_image(" update the first parameter, i.e replace the "annotated label" with your annotated label
	
    c.in load_mask function , in 106th line "image_info["source"] !" , replace the "annotated label" with your annotated label.
    
    d.in image_reference function, in 126th line,replace the "annotated label" with your annotated label.
    
5.Place the custom1.py file in folder where JSON_TO_MASK_V1.ipynb is present.
 
 JSON_TO_MASK_V1.ipynb helps to create ground truth inside train_masked.
  
6.In JSON_TO_MASK_V1.ipynb,following changes need to be performed:

  a.update custom_DIR to the root directory (exclude train directory)
  
  b.In the next cell, which has os.chdir , update the root directory path along with train masked:
    example:root directory/train_masked
    
7.Execute the JSON_TO_MASK_V1.ipynb file, the binary masked ground truth image will be generated inside train_masked folder
	
Please feel free to reach out to me if you have any issues in executing the above steps.

References:

1.https://towardsdatascience.com/cnn-application-detecting-car-exterior-damage-full-implementable-code-1b205e3cb48c

2.http://www.robots.ox.ac.uk/~vgg/software/via/ 

3.https://github.com/matterport/Mask_RCNN/
