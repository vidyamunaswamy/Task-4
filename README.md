# Task-4
import numpy as np

def linear_regression_normal_equation(X, y):
    """
    Computes linear regression coefficients using the Normal Equation.

    Parameters:
        X : list of lists
            Feature matrix (include a column of 1's for the intercept).
        y : list
            Target values.

    Returns:
        list
            Regression coefficients rounded to 4 decimal places.
    """

    # Convert inputs to NumPy arrays
    X = np.array(X, dtype=float)
    y = np.array(y, dtype=float)

    # Step 1: Compute the transpose of X
    XT = X.T

    # Step 2: Compute XᵀX
    XTX = XT @ X

    # Step 3: Compute the inverse of XᵀX
    XTX_inv = np.linalg.inv(XTX)

    # Step 4: Compute Xᵀy
    XTy = XT @ y

    # Step 5: Compute coefficients
    # θ = (XᵀX)⁻¹ Xᵀy
    theta = XTX_inv @ XTy

    # Step 6: Round each coefficient to 4 decimal places
    theta = [round(float(value), 4) for value in theta]

    return theta


# ---------------- Example ----------------

X = [
    [1, 1],
    [1, 2],
    [1, 3]
]

y = [1, 2, 3]

coefficients = linear_regression_normal_equation(X, y)

print("Regression Coefficients:", coefficients)
