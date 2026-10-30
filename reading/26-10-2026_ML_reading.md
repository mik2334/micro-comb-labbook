Reading for the ML section of the literature review (feature-based ML, deep learning on spectra, ML in laser systems)

Part 1: how methods work
**Decision tree**
- flowchart of yes/no questions on the features 
- questions and thresholds are chosen during training to best separate labelled classes
- for my project: data-driven equivalent of the Suresh threshold method 

**Random forest**
- many decision trees, each trained on random subset of the data and features; trees take majority vote
- averaging many trees reduces overfitting 
- gives feature importances: which input the forest relied on most
- for my project: shows which of the Suresh metrics actually matter

**Support vector machine (SVM)**
- treat each map as a point in feature space 
- SVM finds boundary between classes that maximises the margin to the nearest training points
- soft margin: some points are allowed inside the margin/wrong side; setting C controls how strict this rule is
- kernel: implicitly maps the features into a higher-dimensional space; flat boundary there is curved in original feature space
- for my project: smooth boundaries vs box-shaped regions of trees. requires standardised features 

**Neural networks**
- layers of simple units; each takes a weighted sum of its inputs and passes through a non-linear function
- training adjust the weights so the network predicts the correct class
- deep learning - neural networks with many layers

**Convolutional neural network**
- neural network whose early layers use small learned filters along the input; each filter resonds to a local pattern (e.g. sharp peak, broad hump)
- filters are trained together with the final classification layers, so network decides which patterns are useful
- one filter is reused across whole spectrum, so pattern is detected wherever it occurs
- stacked layers build on simple local features to broader patterns
- for my project: learns its own features from raw spectra instead of using the six metrics

Part 2: Notes from papers

**Feature-based classification (method 2)**
James, Witten, Hastie, Tibshirani & Taylor (2023), An Introduction to Statistical Learning with Applications in Python, Springer. [Textbook]
- Ch. 8 (trees, random forests) and ch. 9 (SVMs) used to understand the methods in part 1

Breiman (2001), "Random Forests", Machine Learning 45, 5–32. [Textbook]
- Point in review: random forests combine many trees, each trained on a random subset of data and features, with a majority vote that reduces overfitting

Cortes & Vapnik (1995), "Support-vector networks", Machine Learning 20, 273–297. [Textbook]
- Point in review: SVMs find the maximum-margin boundary with a soft margin; a kernel allows curved boundaries; give smooth boundaries in contrast to tree-based methods

Yang et al. (2023), "Data mining techniques on astronomical spectra data – II. Classification analysis", MNRAS 518(4), 5904–5928. [Abstract + summary]
- Review of spectral classification in astronomy: methods grouped into ten types; nine common algorithms benchmarked across six groups of datasets
- Point in review: classification methods perform differently on different data, no single method is best; motivates comparison of methods; CNN reached highest accuracy on 1D spectra, but with longer training times and tendency to overfit

**Deep learning on spectra (method 3)**
Bishop (2006), Pattern Recognition and Machine Learning, Springer. [Textbook]
- Point in review: general description of a neural network (layers of units, weighted sums, nonlinear functions) ch. 5

Ho et al. (2019), "Rapid identification of pathogenic bacteria using Raman spectroscopy and deep learning", Nature Communications 10, 4927.
- 1D CNN on noisy Raman spectra, 30 bacterial and yeast classes
- Point in review 82.2% accuracy on the 30-class task, vs 75.7% for logistic regression and 74.9% for an SVM, so a CNN outperformed classical baselines on noisy spectra
- used strided convolutions instead of pooling to preserve peak positions 

Képeš et al. (2024), "Interpreting convolutional neural network classifiers applied to laser-induced breakdown optical emission spectra", Talanta 266, 124946.
- neural networks are applied in spectroscopy as black boxes 
- after training, author applies post-hoc interpretation to simplest possible CNN
- CNN predominantly learned physically meaningful features (emission lines of elements in major oxides)
- Point in review: drawback of CNN is that learned features are not directly accessible, but shown that post0hoc interpretation showed the CNN had learned physically meaningful features

**ML methods applied to laser systems** 
Genty et al. (2021), "Machine learning and applications in ultrafast photonics", Nature Photonics 15, 91–101.
- Point in review: ML is already used in the design and operation of pulsed lasers and in characterising and controlling ultrafast propagation dynamics

Kokhanovskiy et al. (2019), "Machine learning methods for control of fibre lasers with double gain nonlinear loop mirror", Scientific Reports 9, 2916.
- first experimental demonstration of ML controlling pulsed regimes of fibre laser with two amplifying loops
high-power fibre lasers often have multiple equilibrium states, makes it hard to reproduce and manage
- Point in review: ML for control of laser regimes rather than classification; shows importance of recognising states in practice. 