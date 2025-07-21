# PEAS/Agent Analysis

## PEAS 

| Component        | Description                                                                                                                                                                                                                                                                                  |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Performance Measure** | The agent’s performance will be evaluated using multiple complementary metrics: <br>- *Accuracy* of rating predictions within ±1 star of the actual rating, accounting for subjective variation.<br>- *Precision* and *Recall* for review helpfulness classification to assess correct identification of helpful reviews.<br>- *Mean Absolute Error (MAE)* for quantifying average magnitude of rating prediction errors. |
| **Environment**         | The agent operates within the Amazon Books Reviews Dataset environment, which contains ~3GB of historical review data with millions of user reviews and book metadata. This environment is static and partially observable, since user profiles and reading histories are incomplete. The environment reflects randomness in user preferences and review helpfulness.                            |
| **Actuators**           | The agent’s actuators produce predictions and recommendations, including:<br>- Rating predictions on a 1–5 star scale with confidence intervals.<br>- Helpfulness scores classifying reviews as "helpful" or "not helpful" along with probability estimates.<br>- Recommendation lists ranking books personalized to each user based on predicted ratings.                                                           |
| **Sensors**             | The agent receives input from multiple modalities:<br>- *User features:* IDs, profile names, historical review patterns.<br>- *Book features:* Genre, author, price, publication date, description.<br>- *Review features:* Text length, sentiment, rating, timestamp.<br>- *Social features:* Helpfulness votes, total rating counts indicating popularity and credibility.                                          |

---

### Problem  
Online book platforms face a major challenge: predicting which books users will rate highly and which reviews will be most helpful to other customers. With millions of books available, customers rely heavily on ratings and reviews to make purchasing decisions, but not all reviews are equal. This creates a complex recommendation environment where platforms must navigate uncertainty about user preferences while ensuring that the most valuable reviews are highlighted to aid customer decision-making.

### Why Uncertainty Modeling is Important  
Uncertainty modeling is crucial for this problem because the data inherently contains multiple sources of uncertainty that significantly impact prediction accuracy. Most users only review a small fraction of the books they read, creating uncertainty about their true preferences and reading patterns. Reading preferences vary greatly between individuals based on genre preferences, reading experience, and personal taste, making it difficult to generalize from limited user data. Some reviews are more informative and helpful than others, but this helpfulness depends on multiple factors, including the reviewer's expertise, writing quality, and the relevance of their perspective to other readers. User preferences and review patterns also change over time, introducing temporal uncertainty that static models cannot capture. Additionally, we often lack complete information about user demographics, reading history, or the context in which they read specific books, creating additional layers of uncertainty that must be modeled probabilistically.



# Agent Setup, Data Preprocessing, Training Setup
## Key Variables
- **User_Preference_Profile (latent):** Represents the hidden reading preferences of each user, inferred from review patterns.
- **Book_Genre:** Categorical observable variable indicating the genre of a book.
- **Rating_Prediction:** Target variable representing the rating a user gives to a book, on a scale from 1 to 5 stars.
- **Review_Quality (latent):** Represents the intrinsic quality of a review, capturing writing quality and expertise.
- **Review_Helpfulness:** Observable binary variable indicating whether a review is helpful (1) or not (0).
- **Book_Popularity:** Observable variable derived from the total ratings count, indicating popularity levels (e.g., Low, High).
- **Review_Length:** Observable categorical variable describing review length as Short, Medium, or Long based on word count.
  
## Connections

- (User_Preference_Profile, Review_Quality) capture hidden factors that influence observable variables.
- Observable nodes (e.g., Book_Genre, Review_Helpfulness, Review_Length) provide measurable input features.
- This structure reflects how user preferences influence genre choice and ratings, while review quality affects helpfulness.
- The model’s hierarchical structure enables reasoning under uncertainty and captures complex relationships.

## Parameter Calculation Process

**Conditional Probability Tables (CPTs)** are estimated primarily using **Maximum Likelihood Estimation (MLE)** for observed variables with sufficient data.  
  
- Parameter estimation is supported by **pgmpy** (Python library for probabilistic graphical models), which provides implementations of Bayesian networks, EM algorithm, and CPT computation.


---



---

# Train Your Model! (5 pts)

- Include a clean, well-documented portion of your training code.  
- Provide either a code snippet here or link to the relevant section in your notebook.

---

# Conclusion / Results (15 pts)

- **Detailed Results**  
  Describe your results thoroughly, including any helpful visualizations such as heatmaps or confusion matrices (if applicable).  
  Provide numerical results where possible.

- **Interpretation**  
  Interpret what your results mean.  
  If performance is poor, compare against simple baselines like random guessing to contextualize your model's effectiveness.

- **Points of Improvement**  
  Propose specific, thoughtful improvements for your model.  
  Avoid vague statements like "more data" or "use reinforcement learning".  
  Instead, analyze your preprocessing steps, training methods, potential simplifications, dataset biases, or errors that may have impacted performance.  
  Implementation of these improvements is not required unless your model clearly lacks detail or effort.

---

# References

- [pgmpy Documentation](https://pgmpy.org/)
- [Other libraries or resources used]
