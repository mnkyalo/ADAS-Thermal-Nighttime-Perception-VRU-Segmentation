# Annotation Guidelines & Quality Control Criteria

## 1. Pixel-Accurate Instance Segmentation for VRUs
* **Boundary Tightness:** Apply fine-grained polygon vertices around non-rigid human limbs, bicycle spokes, and micro-mobility frames[cite: 5]. Ensure zero dead background space inside the mask to maximize mAP50 evaluation metrics[cite: 5].
* **Thermal Contrast Handling:** Account for dynamic heat radiation through clothing versus bare skin to consistently separate VRU contours from ambient cold road surfaces[cite: 5].

## 2. Mixed-Class Workflow Strategy
* **Polygons vs. Bounding Boxes:** Reserving precise polygons for complex, dynamic road users (`Pedestrian`, `Infrastructure`) while using tight 2D bounding boxes for rigid structural targets (`Vehicle`)[cite: 5].
* **Edge Contact:** Bounding box edges must make exact contact with the extreme visible thermal pixels of vehicle panels and bumpers[cite: 5].

## 3. Layering & Overlap Rules (Z-Index)
* Set spatial Z-index ordering accurately when subjects overlap (e.g., a pedestrian walking in front of a parked vehicle) to prevent label overlap and model hallucination in low-contrast night imagery[cite: 5].
