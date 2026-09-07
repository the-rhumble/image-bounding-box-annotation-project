# Annotation Quality Checks

## 1. Purpose

Quality control was performed after completing the image annotation task to identify inconsistent labels, inaccurate bounding boxes, missed faces, and errors involving ambiguous mask wearing situations.

The objective was to assess whether the annotation guidelines were being applied consistently across the dataset.

---

## 2. Quality Control Sample

A random sample representing approximately 10% of the annotated images was selected for review.

20%

The sample was reviewed independently after the initial annotation pass.


## 3. Review Criteria

Each sampled image was checked against five criteria.

### A. Face Detection

Were all qualifying faces annotated?

Possible outcomes:

```text
Pass
Missed face
```

### B. Bounding Box Accuracy

Was each box sufficiently tight around the visible face?

Possible outcomes:

```text
Pass
Too large
Too small
Poor positioning
```

### C. Class Accuracy

Was the correct mask status assigned?

Possible outcomes:

```text
Pass
with_mask error
without_mask error
mask_weared_incorrect error
```

### D. Multiple Face Handling

Were all visible qualifying faces individually annotated?

Possible outcomes:

```text
Pass
Missed face
Merged faces
Duplicate box
```

### E. Edge Case Handling

Were partially visible, overlapping, side profile, blurred, or incorrectly worn masks handled according to the guideline?

Possible outcomes:

```text
Pass
Guideline inconsistency
Requires review
```

---

## 4. Quality Control Log



Bounding error - I initially mislabelled 5 images, with the boxes covering only the mask on the face and not including the forehead and eyes, this was reviewed and corrected using the annotation guidelines

---

### Bounding Box Error

* excessive background
* included too much hair
* box did not cover the visible face completely


Quality Control Summary


### Sample reviewed

```text
Images reviewed: 10
Total annotations reviewed: 49
```

### Errors identified

```text
Bounding box errors: 2
Classification errors: 0
Missed faces: 0
Duplicate annotations: 0
Ambiguous cases requiring guideline clarification: 1
```

### Corrections made

```text
Bounding boxes corrected: 2
Labels corrected: 0
Missed face annotations added: 0
Duplicate annotations removed: 0
Guideline updated: Yes
```

---

# 7. Error Rate


```text
Error Rate = Images With Errors / Images Reviewed × 100
```


```text
3 / 10 × 49 = 14.7%
```

---

# 8. Common Error Analysis


> The most common error involved bounding boxes too large, this was trimmed to fit more closely



