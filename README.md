## TensorFlow - Help Protect the Great Barrier Reef

![image](https://user-images.githubusercontent.com/67547213/153533915-b1cf14db-326d-4eaf-b98a-d78e584c0604.png)

### Summary
- Model 1 (Classifier): EfficientNetV2
    - train with `train_semi_supervised` and Sartorious dataset
    - result: `0.0 losses` and `100% accuracy` on training, validation sets
- Model 2 (Instance Segmentation): Mask R-CNN (R101-FPN)
    - Training stage 1: train with eight-class LIVECell dataset
    - Training stage 2: train with three-class Sartorious dataset with pretrained weights from stage 1
- Inference: use EfficientNetV2 classifier to predict class which is used to refine final prediction of Mask R-CNN
- 5 folds cross-validation
- Ensembling masks from different models with customed Weighted Boxes Fusion

   s = [1, 1, 1, 0.83, 0.83], f = [None, 2, 3, None, 3]
