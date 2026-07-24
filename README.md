# 🚘 ADAS Thermal Nighttime Perception: VRU Instance Segmentation

**Evaluator:** Margaret Kyalo  
**Domain:** Automotive Vision, Autonomous Driving (ADAS), Thermal Infrared (LWIR) Perception  
**Dataset:** Teledyne FLIR Thermal ADAS Dataset v2  
**Tools Used:** CVAT (Computer Vision Annotation Tool), SAM / AI Interactor  

---

## 📌 Project Overview & Technical Context

Standard RGB camera systems in autonomous vehicles frequently fail under low-light conditions, dense fog, and direct headlight glare. To bridge this safety-critical gap, **Long-Wave Infrared (LWIR)** thermal sensors capture heat radiation rather than reflected light, making them ideal for identifying **Vulnerable Road Users (VRUs)** such as pedestrians, cyclists, and skateboarders in zero-visibility environments.

The goal of this project was to perform high-precision, pixel-level **Instance Segmentation** on night-vision datasets in CVAT to prepare high-fidelity ground truth data for edge-AI perception models (e.g., YOLOv7 / YOLOv8) used in collision avoidance systems.

---

## 🛠️ Annotation Methodology & Quality Control

### 1. Pixel-Accurate Instance Segmentation for VRUs
* **Boundary Tightness:** Applied fine-grained polygons around non-rigid human limbs, bicycle spokes, and micro-mobility frames to eliminate dead background space inside the mask, directly increasing $mAP_{50}$ mask evaluation scores.
* **Dynamic Thermal Signatures:** Accounted for variable thermal contrast (e.g., body heat radiating through clothing vs. direct skin exposure) to consistently delineate human boundaries against cold road surfaces.

### 2. Mixed-Class Optimization Workflow
* **Hybrid Geometry Strategy:** Utilized 2D Bounding Boxes for rigid, predictable structural objects (e.g., parked cars, trailers) while reserving fine Polygons for complex, dynamic road users to balance throughput and spatial precision.
* **Extreme Pixel Contact:** Strictly adhered to bounding box edge contact rules, ensuring box boundaries touch the extreme visible thermal pixels of vehicle panels.

---

## 🏷️ Dataset Taxonomy & Custom Attributes

| Class Name | Geometry Type | Target Objects & Visual Features | Custom Attributes & Tags |
| :--- | :---: | :--- | :--- |
| **`Pedestrian`** | Polygon | Dynamic human targets showing high thermal intensity (light gray / white contours). Includes VRUs on micro-mobility devices. | • **Pose:** `Standing`, `Walking`, `Bending`, `Sitting`, `On a device`<br>• **Occlusion:** `True` / `False`<br>• **Device:** `Bicycle`, `Skateboard`, `Scooter`, `None` |
| **`Vehicle`** | Box & Polygon | Rigid motorized bodies, heated wheel wells, exhaust systems, parked cars, and trailers. | • **Type:** `Sedan`, `SUV`, `Trailer`, `Truck`<br>• **Proximity:** `Foreground`, `Background` |
| **`Infrastructure`** | Polygon | Static background elements, structural walls, lighting posts, and road borders. | • **Type:** `Building_Structure`, `Street_Lamp`, `Signage`, `Bollard_Post`, `Curb_Border`<br>• **Thermal State:** `Active_Heat_Source`, `Ambient_Cold`<br>• **Functionality:** `Navigable_Boundary`, `Physical_Obstacle`, `Illumination` |

---

## 📸 Portfolio Visual Highlights

### 1. Multi-Class VRU Instance Segmentation & Micro-Mobility
CVAT workspace demonstrating pixel-accurate instance segmentation on night-vision LWIR thermal data. High-risk VRUs—a cyclist (left) and skateboarder (right)—are delineated using precise polygons to isolate complex body contours and wheel geometries from background thermal noise.

<p align="center">
  <img src="./assets/CVAT-ADAS_Thermal_Perception_Fig_1.png" alt="VRU Thermal Instance Segmentation" width="850"/>
</p>

*Selected Attributes:* `Pose: On a device` | `Device: Bicycle` | `Occlusion: False`

---

### 2. Pedestrian Pose Tagging & Occlusion Handling
Demonstration of multi-class instance segmentation on nighttime FLIR data. A foreground pedestrian (`Pose: Walking`) positioned beside an RV/trailer is segmented alongside background vehicles using Z-index alignment to prevent label overlap.

<p align="center">
  <img src="./assets/CVAT-ADAS_Thermal_Perception_Fig_2.png" alt="Pedestrian Thermal Instance Segmentation" width="850"/>
</p>

*Selected Attributes:* `Pose: Walking` | `Device: None` | `Type: Trailer`

---

### 3. Infrastructure & Thermal Source Modeling
CVAT workspace illustrating separate polygon masks for structural walls, sidewalk curb borders (`Navigable_Boundary`), and active streetlight posts (`Active_Heat_Source`). This allows ADAS vision stacks to distinguish artificial heat sources from navigable roadways.

<p align="center">
  <img src="./assets/CVAT-ADAS_Thermal_Perception_Fig_3.png" alt="Infrastructure Thermal Instance Segmentation" width="850"/>
</p>

*Selected Attributes:* `Type: Street_Lamp` | `Thermal State: Active_Heat_Source` | `Functionality: Illumination`

---

## 🎯 Key Takeaways & Engineering Impact

* **High-Precision Edge Quality:** Delivered clean polygon masks across dense urban night scenes, drastically reducing false positives caused by background infrared noise.
* **Safety-Critical Focus:** Prioritized accurate classification of high-risk Vulnerable Road Users (VRUs), supporting robust ADAS collision avoidance frameworks.
* **Advanced CVAT Expertise:** Demonstrated expert-level proficiency with multi-class hierarchy management, polygon vertex editing, spatial Z-index ordering, and custom attribute tagging.
