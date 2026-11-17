# econ3916-lab16-regularization
# Regularization: Buying Bias to Sell Variance

## Objective
I tested how penalising the size of coefficients helps a model predict when there are more predictors than useful signal.

## Methodology
- I built a simulated design with 200 predictors, only 5 of them real, and 105 training rows, and fitted OLS, LASSO and Ridge to it.
- I traced the LASSO path to see which variables enter as the penalty shrinks.
- I chose the penalty by 5-fold cross-validation, with the scaler fitted inside every fold.
- I scored LASSO's selection against the known truth.
- I gave LASSO and Ridge two near-duplicate predictors to see how each handles them.
- I compared Elastic Net with LASSO and Ridge on the near-duplicate design.
- I tested what happens to LASSO and OLS when one predictor is measured on a scale 1,000 times larger.
- I wrote my own prompt asking an AI for the cross-validation loop, and checked its lambda and CV MSE against mine.

## Key Findings
- Test MSE was 12.9587 for OLS, 10.1128 for Ridge, and 1.4219 for LASSO. OLS fit the training rows perfectly but failed on new data; on this sparse design, LASSO cut the test error by 89% and Ridge by 22%.
- On the LASSO path, all five true predictors were in from step 6, and the first noise variable entered at step 17.
- 5-fold cross-validation chose lambda = 0.1995, with a CV MSE of 1.5502.
- LASSO found all 5 of the 5 true predictors, along with 11 false positives.
- With two near-duplicate predictors, LASSO put 4.462 on one and zero on the other; Ridge split the weight, 1.618 and 1.609. Elastic Net chose pure LASSO and matched its test MSE of 1.1055, against 10.8464 for Ridge.
- Without standardisation, LASSO kept only 2 variables and its test MSE rose to 19.6219; with it, the test MSE was 1.4219. OLS changed too, from 12.9587 to 10.7377, because with more predictors than rows it also depends on scale.
- My AI prompt took 2 rounds. The AI's loop matched Step 6 in every digit both times: lambda 0.1995 and CV MSE 1.5502 on all 21 penalties, and lambda 0.1585 and CV MSE 1.5810 on every second one.
