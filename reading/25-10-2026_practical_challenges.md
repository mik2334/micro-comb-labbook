Reading for the "practical challenges" section of the literature review (label noise, class imbalance, fair evaluation, preprocessing). Notes written in the physical lab book on 25th Oct 2026.

**Approach** 
For each challenge, notes follow the same pattern as the review paragraph: problem -> evidence -> why it applies to this project

1. Label noise
Frénay & Verleysen (2014), "Classification in the presence of label noise: a survey", IEEE Transactions on Neural Networks and Learning Systems 25(5), 845–869.
- Problem: label noise = observed class labels differ from the true classes ( as distinct from noise in the features)
- Sources: labels from automated rules or insufficient information; subjective or expert labelling 
- Noise types: taxonomy of random, class-dependent and feature-dependent noise
- Consequences: lower classification accuracy; mroe complex learned models; distorted feature importance; misleading if test labels are also noisy 
- Classifier sensitivity: impact differs between classifier types; in one, SVMs did poorly, attributed to reliance on support vectors; results are inconsistent between studies, robustness must therefore be tested
- Responses: noise-robust models; cleaning training data; algorithms that model noise
- Points for review; noisy labels arise from automated rules and reduce accuracy, increase complexity and distort feature importance;
- Applies to project: 
    - Suresh labels come from thresholds derived from the statistical distribution of the data, so errors will be near state boundaries 
    - Boundaries are physical boundaries; states may genuinely be ambiguous 
    - Hand labels are subjective, so neither sourse is ground truth

2. Class imbalance 
He & Garcia (2009), "Learning from imbalanced data", IEEE Transactions on Knowledge and Data Engineering 21(9), 1263–1284.
- Problem: most learning algorithms assume balanced classes and equal misclassification costs
- Consequences: bias towards majority class; poor recall on minority; misleading high overall accuracy 
- Responses:
    - Sampling: random over/undersampling, informed undersampling, synthetic oversampling, cleaning methods
    - cost-sensitive learning (weighting)
    - kernel-based methods
    - evaluation with precision, recall, F1 score
- Point in review: imbalance biases classifiers and hides poor minority detection behind high accuracy; remedies are as stated above
- Applies to project: 
    - Solitons only exist in a limited region of pump-delay space, so they are likely a minorty class, and near boundaries will overlap with neighbouring states 
    - Soliton detection is arguably what matters most 
- Methodology notes: compare no mitigation vs class weighting vs one resampling method; class weighting for the CNN; resample training set only 

3. Fair evaluation/data leakage
Kapoor & Narayanan (2023), "Leakage and the reproducibility crisis in machine-learning-based science", Patterns 4(9), 100804.
- Problem: data leakage = information from the test data influencing training
- Consequences: over-optimistic performance; affected many published studies across fields
- Taxonomy: no clean train-test separation (preprocessing or feature selection fitted on all data duplicates across splits); test samples not independent of training samples
- Response: "model info sheets" documenting why each leakage type does not occur
- Point in review: leakage tends to over-optimistic performance; common causes are preprocessing on full dataset
- Applies to project: same pump-delay points are measured in all three maps; preprocessing and resampling fitted to training data only; Suresh thresholds are derived from full dataset, so evaluating method 1 on a test set that helped inform them mey be a form of leakage

Roberts et al. (2017), "Cross-validation strategies for data with temporal, spatial, hierarchical, or phylogenetic structure", Ecography 40(8), 913–929.
- Problem: with dependence in the structure, random cross-validation puts near-copies of test points in the training set 
- Consequences: prediction error underestimated; overfitting hidden; overly complex models favoured
- Response: blocked cross-validation along the dependence structure, with blocks larger than the correlation range
- Point in review: random CV underestimates error for structured data; blocked splitting gives more realistic estimate
- Applies to project: 
    - state changes continuously with pump and power delay, so neighbouring map points are strongly correlated
    - use blocks of the pump x delay map, same for all three maps 

4. Preprocessing
Ho et al. (2019), "Rapid identification of pathogenic bacteria using Raman spectroscopy and deep learning", Nature Communications 10, 4927.
- Preprocessing (Methods, "Raman measurements")
    - per-spectrum background correction (5th order polynomial fit)
    - outlier removal: 25 highest-intensity spectra discarded 
    - cropped to 381.98-1792.4cm^-1
    - per-spectrum min-max normalisation to 0-1
    - no denoising: CNN works directly on low-SNR spectra
- Architecture: strided convolutions instead of pooling to preserve peak positions
- Changing measurement conditions: when optical efficiency degraded, acquisition time was increased (1s -> 2s) and the pre-trained CNN fine-tuned on a new small dataset
- Point in review: example of standard spectral preprcoessing and of adapating changed measurement conditions by fine-tuning
- Applies to project: 
    - Spectra share one wavemnumber axis; my optical data are recorded at different wavelength resolutions, so require resampling onto a common grid
    - per-spectrum normalisation removes absolute power, which varies with pump power and may carry info about the state -> test un-normalised/normalised
    - comb-line spacing is much larger than both OSA resolutions, so individual lines are resolved in all maps 