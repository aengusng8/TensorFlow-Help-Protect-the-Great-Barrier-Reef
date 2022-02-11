## TensorFlow - Help Protect the Great Barrier Reef

![newplot](https://user-images.githubusercontent.com/67547213/153533484-ec87720f-26b8-4bbe-a319-76ea4eb7e771.png)
![image](https://user-images.githubusercontent.com/67547213/153533582-18d09cef-568e-4ae5-b6e7-9463886ffa6d.png)

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
