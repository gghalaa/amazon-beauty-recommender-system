# Amazon Beauty Recommender System

A recommender systems and machine learning project that evaluates recommendation performance on highly sparse e-commerce data. The project uses the Amazon All Beauty dataset and focuses on Bayesian Personalized Ranking Matrix Factorization (BPR-MF) to study how implicit and explicit feedback influence Top-K recommendation performance.

The project investigates how sparse user-item interactions and noisy negative feedback affect recommendation quality.

## Dataset

The project uses the Amazon All Beauty dataset, which contains product reviews and ratings from Amazon product data.

The cleaned dataset used in the project is:

`All_Beauty_5_minimal_cleaned_v2.xlsx`

Dataset statistics:

- 991 users
- 85 products/items
- 5,269 interactions
- Rating scale from 1 to 5
- Highly sparse user-item interactions
- Beauty and cosmetics product domain

The dataset contains the following main information:

- User identifier
- Product/item identifier
- Rating
- Timestamp

The project focuses on a sparse version of the dataset in which most users interact with only a small number of products.

## Project Aim

The main aim of this project is to evaluate how recommendation models perform when user-item interaction data is highly sparse.

The project focuses on:

- Sparse e-commerce recommendation
- Collaborative filtering
- Bayesian Personalized Ranking Matrix Factorization
- Implicit feedback
- Explicit positive and negative feedback
- User and item embeddings
- Top-K recommendation
- Ranking performance
- Recommendation robustness
- Feedback noise

## Problem Focus

The project examines several challenges commonly found in recommender systems.

### Data Sparsity

Most users interact with only a small number of products, creating a sparse user-item interaction matrix and making preference learning more difficult.

### Limited Sequential Information

The dataset contains timestamps, but user interaction histories are relatively short, limiting the usefulness of complex sequential recommendation models.

### Feedback Quality

Low ratings are relatively limited and can introduce noise when they are treated as explicit negative feedback.

### Recommendation Robustness

The project evaluates whether recommendation performance remains reliable when different feedback assumptions are used.

## Experimental Questions

The experimental component focuses on the following questions:

### RQ1

How well can BPR-MF generate Top-K recommendations using implicit positive feedback?

### RQ2

Does including explicit negative ratings improve recommendation performance?

### RQ3

How does sparse interaction data influence ranking performance?

### RQ4

Which feedback approach provides more reliable recommendations under sparse conditions?

## Methods

The project follows a recommender-system workflow that includes:

- Data loading and cleaning
- Selection of relevant user-item interaction features
- Conversion of ratings into implicit interactions
- User-item interaction modeling
- Temporal train-test splitting
- User and item embedding initialization
- BPR-MF model training
- Negative sampling
- Top-K recommendation generation
- Ranking evaluation
- Comparison of implicit and explicit feedback approaches
- Results visualization
- Interactive recommendation interface

## Data Preprocessing

The preprocessing stage includes:

- Keeping user ID, item ID, rating, and timestamp information
- Removing unnecessary columns
- Sorting interactions chronologically
- Converting ratings of 4 or 5 into positive interactions
- Treating unrated items as potential negative samples in the implicit-feedback experiment
- Creating user and item mappings
- Constructing user-item interaction data for model training
- Applying an 80/20 temporal train-test split for each user

The earliest 80% of interactions are used for training, while the most recent 20% are used for testing.

## Recommendation Model

### Bayesian Personalized Ranking Matrix Factorization (BPR-MF)

The implemented recommender uses Bayesian Personalized Ranking with Matrix Factorization.

BPR-MF learns latent representations for users and products and optimizes the model so that products a user interacted with are ranked above products the user did not interact with.

The model configuration includes:

- 128 latent factors
- 30 training epochs
- Learning rate of 0.05
- L2 regularization of 0.001

During training, the model samples:

- A user
- A positive product the user interacted with
- A negative product the user did not interact with

The model then updates the user and item embeddings so that the positive product receives a higher recommendation score.

## Feedback Experiments

Two BPR-MF configurations were evaluated.

### Experiment 1: Implicit Feedback

Ratings of 4 or 5 are treated as positive interactions.

Products that the user has not interacted with are used as potential negative samples.

This approach focuses on learning from positive user behavior rather than assuming that lower ratings always represent reliable negative preferences.

### Experiment 2: Explicit Positive-Negative Feedback

The second experiment directly incorporates rating information:

- Ratings ≥ 4 = positive
- Ratings ≤ 3 = negative

This experiment tests whether explicit low ratings provide useful negative signals for recommendation learning.

## Evaluation Metrics

The models were evaluated using standard Top-K recommendation metrics.

### HR@10 — Hit Rate

Measures whether the correct product appears anywhere in the user's Top-10 recommended products.

### NDCG@10 — Normalized Discounted Cumulative Gain

Rewards the model for ranking the correct product closer to the top of the recommendation list.

### MRR — Mean Reciprocal Rank

Measures how early the first relevant product appears in the ranked recommendation list.

## Results

The two feedback approaches produced substantially different results.

| Metric | Implicit BPR-MF | With Negative Ratings |
|--------|-----------------|-----------------------|
| HR@10 | 0.4224 | 0.11 |
| NDCG@10 | 0.2350 | 0.04 |
| MRR | 0.1730 | 0.02 |

## Key Findings

The main findings of the project include:

- Implicit-feedback BPR-MF performed substantially better than the version using explicit negative ratings.
- The correct product appeared in the Top-10 recommendations approximately 42% of the time in the implicit-feedback experiment.
- Adding explicit negative ratings reduced HR@10 to approximately 11%.
- NDCG@10 and MRR also decreased substantially when explicit negative ratings were introduced.
- Positive-only interaction data provided a more reliable learning signal under highly sparse conditions.
- Low ratings were too limited and noisy to improve ranking performance.
- Sparse datasets can make recommendation models sensitive to how positive and negative feedback are defined.
- BPR-MF provided a strong baseline for recommendation under sparse e-commerce conditions.

## Research Context

The project also reviews several important recommender-system architectures and research directions, including:

- Matrix Factorization
- Neural Collaborative Filtering (NCF)
- Factorization Machines
- GRU4Rec
- SASRec
- BERT4Rec
- Neural Graph Collaborative Filtering (NGCF)
- LightGCN
- Self-Supervised Graph Learning (SGL)
- CL4SRec
- SimGCL
- PinSAGE
- RecBole

These models were studied to understand the development of sequential, graph-based, and contrastive recommender systems.

The experimental implementation in this repository focuses specifically on BPR-MF. The other architectures are discussed as research context and possible directions for extending the system.

## Technologies Used

- Python
- Jupyter Notebook
- Google Colab
- pandas
- NumPy
- Matplotlib
- Gradio

## Project Structure

```text
amazon-beauty-recommender-system/
├── notebook/
│   └── AMAZONFINAL.ipynb
├── report/
│   └── Evaluating Recommendation Techniques.pdf
├── presentation/
│   └── AI Presentation.pptx
├── references/
│   └── Information Table LR.pdf
└── README.md
```

## Main Files

- `AMAZONFINAL.ipynb` - Main Jupyter Notebook containing data preprocessing, BPR-MF training, recommendation evaluation, visualizations, and the interactive recommendation interface
- `Evaluating Recommendation Techniques.pdf` - Final project report covering recommender-system research, methodology, experiments, results, and analysis
- `AI Presentation.pptx` - Project presentation summarizing the problem, dataset, methodology, results, and conclusions
- `Information Table LR.pdf` - Literature review reference table comparing major recommender-system models and research
- `README.md` - Project overview and instructions

## How to Run the Project

1. Clone or download this repository.

2. Open the project folder.

3. Open the Jupyter Notebook:

   `notebook/AMAZONFINAL.ipynb`

4. Install the required Python libraries if needed:

   `pip install pandas numpy matplotlib gradio openpyxl`

5. Obtain the Amazon All Beauty dataset used by the project.

6. Make sure the cleaned dataset file is available to the notebook:

   `All_Beauty_5_minimal_cleaned_v2.xlsx`

7. Update the dataset path in the notebook if necessary.

8. Run the notebook cells in order.

## Notes

- The dataset is highly sparse, making it useful for studying recommender-system performance under limited user interactions.
- The project focuses on ranking products rather than predicting exact star ratings.
- The implemented model is BPR-MF.
- LightGCN, BERT4Rec, SimGCL, and other advanced models discussed in the report are part of the research and conceptual framework and are not implemented in the experimental notebook.
- Implicit feedback produced substantially better ranking results than explicitly including low ratings as negative interactions.
- The project demonstrates that feedback design can significantly influence recommendation performance under sparse conditions.
- BPR-MF provides a useful baseline for future extensions using graph-based, sequential, or contrastive recommendation techniques.

## Authors

- Ghala Alghamdi
- Hiba Amanulla
- Effat University
- Computer Science Department
- Course: CS3081 – Artifical Intelligence
- Instructor: Dr. Passent Elkafrawy
