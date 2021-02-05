# Detect and mitigate unfairness in models with Azure Machine Learning

Machine learning models are increasingly used to inform decisions that affect people's lives. For example, a prediction made by a machine learning model might influence:

* Approval for a loan, insurance, or other financial services.
* Acceptance into a school or college course.
* Eligibility for a medical trial or experimental treatment.
* Inclusion in a marketing promotion.
* Selection for employment or promotion.

With such critical decisions in the balance, confidence that the machine learning models we rely on predict, and don't discriminate for or against subsets of the population based on ethnicity, gender, age, or other factors.

![](../Images/Unfairness.PNG)

## Learning objectives
In this module, you will learn how to:

* Evaluate machine learning models for fairness.
* Mitigate predictive disparity in a machine learning model.

## Consider model fairness

When we consider the concept of *fairness* concerning predictions made by machine learning models, it helps to be clear about what we mean by "fair".

For example, suppose a classification model is used to predict the probability of successful loan repayment and therefore influences whether or not the loan is approved. The model will likely be trained using features that reflect the characteristics of the applicant, such as:

* Age
* Employment status
* Income
* Savings
* Current debt

These features are used to train a binary classification model that predicts whether an applicant will repay a loan.

![](../Images/Unfairness1.PNG)

Suppose the model predicts that around 45% of applicants will successfully repay their loans. However, on reviewing loan approval records, you begin to suspect that fewer loans are approved for applicants aged 25 or younger than for applicants who are over 25. How can you be sure the model is *fair* to applicants in both age groups?

## Measuring disparity in predictions
One way to start evaluating the fairness of a model is to compare *predictions* for each group within a *sensitive feature*. For the loan approval model, *Age* is a sensitive feature that we care about, so we could split the data into subsets for each age group and compare the *selection rate* (the proportion of positive predictions) for each group.

![](../Images/Unfairness2.PNG)
