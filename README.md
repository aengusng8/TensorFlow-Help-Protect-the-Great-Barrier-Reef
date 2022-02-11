## TensorFlow - Help Protect the Great Barrier Reef

![image](https://user-images.githubusercontent.com/67547213/153533856-5d6a1982-5860-4eaf-aa43-43ceaecb5b0e.png)

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
