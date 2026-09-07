# Face Mask Detection Bounding Box Annotation Guidelines

## 1. Purpose

The purpose of this annotation project is to create a consistent object detection dataset containing human faces and their mask wearing status.

Each visible face should receive one bounding box and exactly one class label:

* `with_mask`
* `without_mask`
* `mask_weared_incorrect`

The bounding box should identify the visible face rather than the entire head, hair, neck, shoulders, or body.

These guidelines should be followed consistently throughout the dataset.

---

## 2. Annotation Unit

The annotation unit is the **visible human face**.

For every qualifying face:

1. Draw one bounding box.
2. Make the box as tight as reasonably possible around the visible face.
3. Assign exactly one mask status label.
4. Do not create multiple boxes for the same face.
5. Do not annotate unrelated objects.

The objective is consistency rather than attempting to estimate hidden facial boundaries.

---

## 3. Bounding Box Rules

### 3.1 What the box should contain

The bounding box should cover the visible facial region.

Include:

* forehead when visible
* eyes
* nose
* cheeks
* mouth or mask area
* chin when visible

Exclude as much as possible:

* hair
* neck
* shoulders
* clothing
* background
* unrelated objects

The box should be tight enough that unnecessary background is minimised.

### 3.2 Tight box principle

Use the smallest practical rectangle that contains the visible face.

Do not deliberately create oversized boxes around the person's entire head.

### Example

Correct:

```text
+----------------+
|    forehead    |
|   eyes         |
|   nose         |
|   mask         |
|   chin         |
+----------------+
```

Incorrect:

```text
+----------------------+
|        hair          |
|     +----------+     |
|     |   FACE   |     |
|     +----------+     |
|                      |
|       neck           |
+----------------------+
```

---

# 4. Class Definitions

## 4.1 with_mask

Use `with_mask` when the person is wearing a face mask correctly.

A correctly worn mask generally covers both:

* nose
* mouth

Examples include:

* surgical masks covering the nose and mouth
* cloth masks covering the nose and mouth
* medical masks
* other clearly visible protective face coverings

If the mask is visibly positioned over both the nose and mouth, label it:

```text
with_mask
```

---

# 4.2 without_mask

Use `without_mask` when the person is not wearing a mask.

Examples include:

* completely uncovered face
* visible nose and mouth without a mask
* mask clearly absent
* person holding a mask rather than wearing it

If a person has a mask in their hand, around their neck, or somewhere else on their body but it is not covering their face, the face should normally be labelled:

```text
without_mask
```

---

# 4.3 mask_weared_incorrect

Use `mask_weared_incorrect` when a mask is being worn but is clearly positioned incorrectly.

Examples include:

* mask covering mouth but not nose
* mask sitting below the mouth
* mask covering only part of the required facial area
* mask hanging from one ear while still visibly associated with the face
* mask positioned under the chin

The important distinction is:

**Mask present but incorrectly positioned = `mask_weared_incorrect`.**

**No mask being worn = `without_mask`.**

---

# 5. Partially Visible Faces

Annotate a partially visible face when enough of the face is visible to reasonably determine that it is a face and assign a mask status.

Examples include:

* face partially cut off by the image boundary
* side profile
* face partially hidden by another person
* face partially obscured by an object

The bounding box should cover the visible facial region.

Do not attempt to estimate large hidden areas.

### Example

If only approximately half of a face is visible at the edge of the image, draw the box around the visible portion rather than extending the box beyond the image.

---

# 6. Faces at the Image Boundary

If a face continues outside the image, annotate the visible portion.

The bounding box should touch the relevant image boundary.

Do not invent the location of the hidden portion.

For example, if a face enters from the right side:

```text
+--------------------------+
|                    +-----|
|                    |face |
|                    |     |
|                    |     |
+--------------------+-----+
```

The box should terminate at the image boundary.

---

# 7. Side Profile Faces

Side profile faces should be annotated when the facial region is sufficiently visible.

A side profile is still a face.

Do not automatically classify a side profile as `without_mask` simply because the mask is difficult to see.

Instead, inspect the visible facial region carefully.

If a mask is clearly visible and correctly positioned:

```text
with_mask
```

If no mask is visible and the face is sufficiently clear:

```text
without_mask
```

If a mask is visibly present but incorrectly positioned:

```text
mask_weared_incorrect
```

If the image quality makes the mask status genuinely impossible to determine, follow the project's ambiguity rule and flag the image for review rather than making an unsupported assumption.

---

# 8. Overlapping Faces

When multiple people appear in an image, annotate each qualifying face separately.

For example:

```text
Person 1 → with_mask
Person 2 → without_mask
Person 3 → with_mask
```

Each face receives its own bounding box.

Do not create one large bounding box around multiple people.

---

# 9. Heavily Overlapping Faces

If two faces overlap:

1. Identify each visible face separately.
2. Draw one box around each face.
3. Allow boxes to overlap where necessary.
4. Do not merge the boxes into a single annotation.

The goal is to represent individual objects rather than visually separate regions.

---

# 10. Very Small Faces

Annotate small faces when they are sufficiently visible to identify the face and determine its class with reasonable confidence.

Do not enlarge the box artificially.

Do not annotate tiny background objects that cannot be reliably identified as faces.

If a face is too small or unclear to determine its mask status reliably, flag it for review.

---

# 11. Blurred or Low Quality Faces

If the face is visible but the image is slightly blurred, annotate it when the face and mask status can still be determined.

Do not attempt to recover information that cannot be seen.

For example:

Blurred but clearly masked:

```text
with_mask
```

Blurred but clearly uncovered:

```text
without_mask
```

Mask visible but clearly incorrectly positioned:

```text
mask_weared_incorrect
```

If the class cannot be determined reliably, flag the image for review.

---

# 12. Masks Around the Chin

A mask positioned below the chin should generally be labelled:

```text
mask_weared_incorrect
```

The reason is that a mask is present and associated with the face, but it is not being worn correctly.

---

# 13. Masks Around the Neck

If a mask is hanging around the neck and the person's face is completely uncovered, classify the face as:

```text
without_mask
```

The mask is not functioning as a face covering.

---

# 14. Masks Covering Only the Mouth

If the mask clearly covers the mouth but leaves the nose exposed:

```text
mask_weared_incorrect
```

The mask is being worn but incorrectly.

---

# 15. Masks Covering Only the Nose

If the mask covers the nose but does not properly cover the mouth:

```text
mask_weared_incorrect
```

---

# 16. Unclear Mask Status

Do not guess when there is insufficient visual evidence.

Use the following decision process:

```text
Is there a visible face?
        |
        Yes
        |
Is a mask visibly present?
        |
   +----+----+
   |         |
  No        Yes
   |         |
without     Is it correctly positioned?
mask         |
       +-----+-----+
       |           |
      Yes          No
       |            |
   with_mask   mask_weared_incorrect
```

If neither the presence nor absence of a mask can reasonably be determined, flag the case for review.

---

# 17. Sunglasses

Sunglasses do not change the mask classification.

For example:

Sunglasses + mask covering nose and mouth:

```text
with_mask
```

Sunglasses + uncovered face:

```text
without_mask
```

Sunglasses + incorrectly positioned mask:

```text
mask_weared_incorrect
```

---

# 18. Facial Obstructions

If an object partially blocks the face, annotate the visible facial area if the face remains identifiable.

Examples:

* hands
* phones
* clothing
* another person
* objects in the foreground

Do not create a box around the obstruction itself.

---

# 19. Non Human Faces

Do not annotate:

* animals
* drawings
* statues
* posters
* photographs displayed inside another photograph
* mannequins

unless the project specifically requires these objects.

The annotation target is a real human face within the source image.

---

# 20. Multiple Faces With Different Classes

Each face must be independently classified.

For example:

```text
Face 1 → with_mask
Face 2 → without_mask
Face 3 → mask_weared_incorrect
```

Do not assign one class to the entire image.

---

# 21. Confidence and Ambiguity Rule

When uncertain, do not immediately choose the most convenient label.

Use this hierarchy:

1. Clear visual evidence
2. Annotation guideline
3. Edge case rule
4. Manual review

The purpose of the project is to produce reliable labels, not simply to maximise the number of completed annotations.

---

# 22. Final Annotation Checklist

Before considering an image complete, confirm:

[ ] Every qualifying face has a bounding box.

[ ] Each face has only one bounding box.

[ ] Boxes are tight around the visible face.

[ ] Boxes do not unnecessarily include hair, neck, shoulders, or background.

[ ] Every face has exactly one class.

[ ] `with_mask` is used for correctly worn masks.

[ ] `without_mask` is used when no mask is being worn.

[ ] `mask_weared_incorrect` is used when a mask is present but incorrectly positioned.

[ ] Partially visible faces have been handled consistently.

[ ] Overlapping faces have separate boxes.

[ ] Unclear cases have been reviewed rather than guessed.

[ ] No unrelated objects have been annotated.

---

# 23. Principle of Consistency

The same visual situation should receive the same label throughout the dataset.

For example, if a mask below the chin is classified as `mask_weared_incorrect` on one image, the same situation should receive the same label elsewhere.

Consistency is more important than personal interpretation.

If an edge case repeatedly causes uncertainty, update this guideline before continuing with the remaining annotations.
