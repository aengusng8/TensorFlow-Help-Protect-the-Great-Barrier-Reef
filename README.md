## TensorFlow - Help Protect the Great Barrier Reef

![image](https://user-images.githubusercontent.com/67547213/153533915-b1cf14db-326d-4eaf-b98a-d78e584c0604.png)

### Summary
- bluish images because of underwater env -> Data enhancement: **CLAHE**.
- small object detection
    - Increase image size that are multiple of 64: 1920, 2240, 2432,...
    - **cuts two last heads** of Yolov5, because they are used to detect large and extremely large object.
- small dataset
    - use square images (resize 1280x720 to 1280x1280) to octuple (x8) number of images in training and validating dataset, and also octuple (x8) number of transforms when using Test time augmentation. Specifically, **using 8 combinations of 3 transforms (Transpose, HorizontalFlip, and VerticalFlip) can create a original and 7 augmented images** (below example).
    
    ![image](https://user-images.githubusercontent.com/67547213/153640886-7e7caae4-0a8d-4139-9a14-633186be644f.png)

    - heavily rotated Mosaic data augmentation (w/o artifact or tiny bounding boxes): RandomCrop -> Rotate -> CenterCrop
    ```python
img4 = np.full((imsize, imsize, 3), 114, dtype=np.uint8)  # base image with 4 tiles
yc, xc = [int(random.uniform(imsize - imsize / 1.44, imsize / 1.44)) for _ in range(2)]

for i, index in enumerate(indices):
    # Load image & label
    img, _, (h, w) = load_image(self, index)
    labels, segments = self.labels[index].copy(), self.segments[index].copy()

    if labels.size:
        labels = xywhn2xyxy(labels[:, 1:], w, h)  # normalized xywh to pixel xyxy format
        segments = [xyn2xy(x, w, h) for x in segments]
        cats = np.zeros(labels.shape[0], dtype=int)
    else: 
        labels, cats = np.array([]), np.array([])

    # place img in img4
    if i == 0:  # top left
        crop_edge = max(int(1.43 * yc), int(1.43 * xc))
        RANDOM_CROP_ROTATED_CENTRER_CROP = A.Compose([  
                                                        A.RandomCrop(height=crop_edge, width=crop_edge, p=1.0), # sqrt(2) < 1.42
                                                        A.Rotate(limit=170, border_mode=1, p=1.0),
                                                        A.CenterCrop(height=yc, width=xc, p=1.0),  
                                                        ], bbox_params=A.BboxParams(format="pascal_voc", label_fields=["bbox_classes"])) 
        transformed = RANDOM_CROP_ROTATED_CENTRER_CROP(image=img, bboxes=labels, bbox_classes=cats)
    ```
       
    - 
        

   s = [1, 1, 1, 0.83, 0.83], f = [None, 2, 3, None, 3]: 
