## TensorFlow - Help Protect the Great Barrier Reef

![image](https://user-images.githubusercontent.com/67547213/153533915-b1cf14db-326d-4eaf-b98a-d78e584c0604.png)

### Summary
- bluish images because of underwater env -> Data enhancement: CLAHE.
- small object detection
    - Increase image size that are multiple of 64: 1920, 2240, 2432,...
    - cuts two last heads of Yolov5, because they are used to detect large and extremely large object.
- small dataset
    - use square images (resize 1280x720 to 1280x1280) to octuple (x8) number of images in training and validating dataset, and also octuple (x8) number of transforms when using Test time augmentation. Specifically, using 8 combinations of 3 transforms (Transpose, HorizontalFlip, and VerticalFlip) creates a original and 7 augmented images (below example).
    - 2 x customed Mosaic data augmentation (deleted tiny bouding boxes)
        + RandomRotate + CenterCrop (w/o artifact) || Transpose (Reflection) + RandomCrop
        + RandomCrop + random x_center and y_center 
    
    ![image](https://user-images.githubusercontent.com/67547213/153640886-7e7caae4-0a8d-4139-9a14-633186be644f.png)

    - 

   s = [1, 1, 1, 0.83, 0.83], f = [None, 2, 3, None, 3]
