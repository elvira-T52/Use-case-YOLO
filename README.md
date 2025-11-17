# YOLO Transfer Learning for UML Use Case Diagram Analysis

Transfer-learned YOLOv3 model for automated detection and verification of UML Use Case diagram elements to ensure coverage with textual use case scenarios.

**Authors**: Timothy Elvira, Lynn Vonder Haar, Priscilla Carbo

## Overview

This project fine-tunes YOLOv3 for object detection on UML Use Case diagrams, enabling automated extraction of diagram elements (actors, use cases, relationships) and subsequent comparison with textual use case scenarios to verify requirement coverage in software engineering documentation.

### Example Detection

![Example Use Case Diagram Detection](https://github.com/user-attachments/assets/283c91fb-ac9a-4ed9-a61f-9609293f710b)

*YOLOv3 detection results showing identified actors (green), use cases (magenta), and extends (red) relationships.*

## Problem Statement

Software requirements validation often requires manual cross-referencing between UML Use Case diagrams and textual scenarios. This project automates the process by:
1. Detecting and classifying use case diagram elements using transfer-learned YOLO
2. Extracting text from detected regions
3. Comparing extracted elements against written use case scenarios
4. Identifying coverage gaps and missing requirements

## Model Architecture

**Base Model**: YOLOv3 (Darknet)  
**Backbone**: Darknet-53 with pre-trained weights (`darknet53.conv.74`)  
**Detection Classes**: 4 custom classes
- Actor
- Use Case
- Includes (relationship)
- Extends (relationship)

### Training Configuration
- **Epochs**: 6000 iterations
- **Learning Rate**: 0.001
- **Confidence Threshold**: 0.2
- **NMS Threshold**: 0.4
- **Input Size**: 416x416
- **Normalization**: IOU: 0.75, OBJ: 1.00, CLS: 1.00

### Transfer Learning Process
1. Clone AlexeyAB's Darknet implementation
2. Load pre-trained Darknet-53 convolutional weights
3. Fine-tune on custom annotated UML Use Case diagram dataset
4. Train with MSE loss on 3 detection layers (scales 82, 94, 106)
5. Save final weights for inference

## Dataset

Custom dataset of annotated UML Use Case diagrams with bounding boxes for:
- Actors (stick figures)
- Use Case ellipses
- Include relationships (dashed arrows)
- Extend relationships (dashed arrows)

Format: Darknet YOLO annotation format

## Performance

Final training metrics (iteration 6000):
- **Average Loss**: 0.411988
- **Average IOU**: ~0.88-0.90 across detection layers
- **Training Time**: ~0.12 hours per 1000 iterations on GPU

The model achieves high accuracy in detecting:
- Individual actors and use cases
- Relationship arrows between elements
- Text regions for subsequent OCR extraction

## Applications

### Requirements Traceability
- Automatically extract use cases from diagrams
- Compare with textual scenario descriptions
- Generate coverage reports

### Documentation Validation
- Verify diagram completeness
- Identify missing actors or use cases
- Ensure consistency between visual and textual requirements

### Automated Testing
- Generate test cases from detected use cases
- Validate system behavior against requirements
- Track coverage throughout development lifecycle

## Future Enhancements

- [ ] Integrate OCR (Tesseract/EasyOCR) for text extraction from detected regions
- [ ] Implement automated comparison with textual use case scenarios
- [ ] Generate coverage matrix (diagram elements vs. scenarios)
- [ ] Support for additional UML diagram types (Sequence, Class, Activity)
- [ ] Web interface for drag-and-drop diagram analysis

## Requirements

```bash
# Core dependencies
pip install opencv-python
pip install numpy

# For training (Google Colab recommended)
- CUDA-enabled GPU
- Darknet framework (AlexeyAB)
```

## Citation

If you use this work in your research, please cite:

```
Elvira, T., VonderHaar, L., Carbo, [Initial]. "Transfer Learning YOLOv3 for UML Use Case 
Diagram Element Detection and Requirements Coverage Analysis."
```

## Acknowledgments

- AlexeyAB's Darknet implementation
- YOLOv3 architecture by Joseph Redmon
- Google Colab for GPU resources

## Contact

For questions or collaboration:
- Timothy Elvira: elvirat@my.erau.edu
