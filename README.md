## Project Overview

This project demonstrates an end to end image annotation workflow for an object detection dataset. The objective was to annotate human faces according to their face mask wearing status using bounding boxes.

The project was completed using CVAT and follows a documented annotation guideline and quality control process.

The final dataset contains approximately **49 annotated images** and **127 total face annotations**.

---

## Business and Technical Problem

For a face mask detection system, simply identifying that a person exists in an image is not sufficient.

The system needs to understand:

1. Where the face is located.
2. Whether a mask is being worn.
3. Whether the mask is being worn correctly.
4. How to handle multiple people within the same image.

This project addresses that data preparation problem by producing bounding box annotations for individual faces.

---

## Project Objective

The objective was to create a consistent object detection dataset containing three classes:

```text
with_mask
without_mask
mask_weared_incorrect
```

Each qualifying face received one bounding box and one class label.

---

## Dataset

The project uses the Face Mask Detection dataset from Kaggle.

Dataset source:

[Face Mask Detection Dataset on Kaggle](https://www.kaggle.com/datasets/andrewmvd/face-mask-detection)

A subset of approximately 49 images was selected for this annotation project.

The images were placed in:

```text
annotation_project_images/
```


## Annotation Tool

The annotation was performed using CVAT.

[CVAT](https://app.cvat.ai/)

CVAT was selected because it provides an interface specifically designed for computer vision annotation and supports bounding box based object detection workflows.

---

## Annotation Classes

| Class                   | Definition                                              |
| ----------------------- | ------------------------------------------------------- |
| `with_mask`             | Face with a mask correctly covering the nose and mouth  |
| `without_mask`          | Face without a mask being worn                          |
| `mask_weared_incorrect` | Face where a mask is present but incorrectly positioned |

---

## Annotation Method

Each image was reviewed individually.

For every qualifying human face:

1. A bounding box was drawn.
2. The box was positioned around the visible facial region.
3. The appropriate mask class was assigned.
4. Multiple faces were annotated separately.
5. Difficult cases were handled according to the annotation guideline.

The bounding boxes were designed to be tight around the visible face covering the mask rather than around the entire head or body.

---

## Annotation Guidelines

The complete annotation rules are available here:

[ANNOTATION_GUIDELINES.md](ANNOTATION_GUIDELINES.md)

The guideline covers:

* bounding box placement
* multiple faces
* overlapping faces
* partially visible faces
* side profiles
* small faces
* blurred images
* masks below the nose
* masks below the chin
* masks around the neck
* ambiguous cases
* non human objects

---

## Quality Assurance

A random sample representing approximately 20% of the dataset was reviewed after annotation.

For a 49 image dataset, this resulted in approximately 10 images being audited.

The audit checked:

* missed faces
* duplicate boxes
* bounding box accuracy
* class accuracy
* multiple face handling
* difficult edge cases

Errors were documented and corrected.

Full details are available in:

[QUALITY_CHECKS.md](QUALITY_CHECKS.md)

---

## Quality Control Results

| Metric                 |    Result |
| ---------------------- | --------: |
| Total images           |  10 |
| Total face annotations |  15 |
| Images audited         |  3 |
| Bounding box errors    | 2 |
| Classification errors  | 0 |
| Missed faces           |  0 |
| Duplicate annotations  |  0 |
| Corrections made       |  2 |
| Final image error rate | 14.7% |

These figures were calculated from the completed annotation and quality control audit.

---

## Key Annotation Challenges

Several situations required additional judgement during annotation.

### Masks below the chin

A mask visibly positioned below the chin was treated as an incorrectly worn mask.

### Multiple people

Each face received its own bounding box and independent class label.

### Partially visible faces

Faces cut off by the image boundary were annotated based on the visible facial region.

### Side profiles

Side profile faces were annotated when there was sufficient visual evidence to identify the face and determine mask status.

---

## Error Analysis

The quality control review was used to identify recurring annotation mistakes.

One of the main objectives was to determine whether errors were isolated mistakes or evidence that the annotation guideline needed clarification.


---

## Screenshots

### CVAT Task

![CVAT task](screenshots/cvat_task.png)

### Annotation Example

![Annotation example](screenshots/annotation_example.png)

### Multiple Faces

![Multiple faces](screenshots/multiple_faces.png)

### Difficult Case

![Difficult case](screenshots/difficult_case.png)

### Completed Annotation Task

![Completed task](screenshots/completed_task.png)


---

## Skills Demonstrated

### Data Annotation

* Bounding box annotation
* Object detection labelling
* Multi object annotation
* Image classification

### Data Quality

* Quality control sampling
* Error identification
* Error categorisation
* Annotation correction
* Consistency checking
* Edge case analysis

### Tools

* CVAT
* GitHub
* Markdown

### Documentation

* Annotation guideline development
* Quality assurance documentation
* Dataset documentation
* Portfolio project documentation

---

## Key Learning Outcomes

The workflow included:

```text
Dataset Selection
       ↓
Image Preparation
       ↓
Guideline Development
       ↓
CVAT Annotation
       ↓
Annotation Review
       ↓
Random Quality Sample
       ↓
Error Analysis
       ↓
Corrections
       ↓
Guideline Improvement
       ↓
Final Dataset
       ↓
Documentation
```

The project therefore demonstrates practical experience with the full annotation and quality control lifecycle.

---

## Limitations

The quality audit was based on a sample rather than a complete independent reannotation of the entire dataset.

The resulting dataset should therefore be treated as an annotated portfolio dataset rather than a formally validated production dataset.

---

## Conclusion

This project demonstrates a structured approach to preparing computer vision training data.

The main focus was consistency, accurate bounding boxes, clear class definitions, systematic quality control, and documentation of ambiguous cases.

The final output can serve as an example of practical image annotation and data quality work for computer vision, machine learning, data operations, and AI data labelling roles.
