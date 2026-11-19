# cbct-dataset-annotation-guide
A practical guide to building training-ready CBCT datasets: annotation types, common challenges, and best practices.
A practical guide for AI teams working with cone-beam CT (CBCT) data in dental and maxillofacial imaging. Raw scans are not a dataset. This guide explains how to turn them into training-ready CBCT datasets that models can learn from reliably.

Contents
What “training-ready” means
Choosing an annotation type
Common challenges and fixes
Best practices
Pre-training checklist
Recommended workflow
About
1. What “Training-Ready” Means

A CBCT dataset is training-ready when a model can learn from it without being misled by noise, inconsistent labels, or data leakage. In practice this means the dataset has:

Labels that follow a written, versioned guideline
Consistent file formats, voxel spacing, and orientation
Fully de-identified patient data
Variety across scanners, protocols, ages, and conditions
Measured agreement between annotators
Patient-level train, validation, and test splits
2. Choosing an Annotation Type

Match the annotation to the clinical task.

Annotation type	What it labels	Typical use
Semantic segmentation	Every voxel by structure	Implant planning, airway analysis, nerve canal tracing
Instance segmentation	Each tooth as a separate object	Tooth numbering, charting, orthodontics
Landmark annotation	Anatomical points in 3D	Cephalometric and symmetry measurements
3D bounding boxes	Cuboid regions	Cysts, impacted teeth, implants, lesions
Classification labels	Scan or region tags	Pathology presence, bone density grade
Surface and mesh models	Smooth 3D surfaces	Prosthetics, aligners, surgical guides
3. Common Challenges and Fixes
Challenge	Why it matters	What to do
Metal and motion artifacts	Streaks hide real anatomy	Define rules for unclear regions and set rejection criteria
Unreliable grayscale values	Thresholding fails across devices	Rely on expert review and normalize carefully
Scanner variability	Models fail on unseen devices	Collect data from multiple scanners and protocols
Inter-annotator disagreement	Becomes label noise	Use guidelines, double reading, and adjudication
Slow 3D labeling	Fatigue causes errors	Use pre-labeling with human verification
Class imbalance	Small structures get ignored	Add targeted samples and suitable loss functions
Privacy risk	DICOM headers and facial features reveal identity	De-identify metadata and review volumes
Data leakage	Inflated test results	Split strictly by patient
4. Best Practices

Define the clinical goal first. Every label class and tolerance should trace back to the decision the model supports.

Write a detailed annotation guideline. Include definitions, boundary rules, artifact handling, and example images. Version it and update it as edge cases appear.

Run a pilot batch. Annotate around 20 scans, measure agreement, and fix unclear rules before scaling.

Combine annotators and clinical experts. Trained annotators handle volume. Dental and radiology specialists set standards and resolve disputes.

Measure quality with real metrics. Track Dice, IoU, and surface distance for segmentation, and Cohen’s kappa for categorical labels.

Double-read critical structures. The inferior alveolar canal and similar high-risk labels deserve consensus review.

Use AI-assisted pre-labeling carefully. It saves time, but every output needs expert verification so model errors are not reinforced.

Standardize formats. Use NIfTI or DICOM-SEG, harmonize orientation and spacing, and document every preprocessing step.

De-identify thoroughly. Clean metadata and confirm compliance with applicable regulations and consent terms.

Split by patient. Keep every scan from one patient in a single split.

Version your data. Track dataset releases, changes, and annotator history just as you would track code.

5. Pre-Training Checklist

Before you start training, confirm that:

[ ] The clinical task and label schema are written down
[ ] An annotation guideline exists and is versioned
[ ] A pilot batch was reviewed and the guideline refined
[ ] Agreement metrics meet your agreed thresholds
[ ] Critical structures had double review
[ ] All patient identifiers were removed from metadata
[ ] Formats, voxel spacing, and orientation are consistent
[ ] Data covers multiple scanners and protocols
[ ] Splits were made at the patient level
[ ] The dataset release is versioned and frozen
6. Recommended Workflow
Define the task and label schema
Collect and de-identify diverse scans
Standardize formats and metadata
Write guidelines and run a pilot
Annotate with pre-labeling and expert review
Run quality checks and adjudicate disagreements
Split by patient and freeze a versioned release
Train, evaluate, and trace model errors back to the data

Step 8 matters most. The best datasets keep improving as the model shows where labels or coverage fall short.

7. About

This guide is maintained by Pariedolia System LLp, which provides medical image annotation and dataset preparation for AI teams, turning raw imaging data into reliable, model-ready assets.

Website: https://pareidolia.in

Contributing

Suggestions and corrections are welcome. Open an issue or submit a pull request with your proposed change.

Disclaimer

This guide is for educational purposes and does not constitute medical or regulatory advice. Always follow the privacy laws and clinical requirements that apply to your region.
