
# Chapter 07 Modernization Notes

## Runtime Environment

The notebook was validated in the following environment:

- Environment: `ml4t-core`
- Python: 3.10.20
- NumPy: 1.26.4
- pandas: 2.2.3
- SciPy: 1.15.2
- scikit-learn: 1.7.2
- statsmodels: 0.14.6
- Matplotlib: 3.10.9
- seaborn: 0.13.2
- JupyterLab: 4.6.2

## Notebook Status

### `01_linear_regression_intro.ipynb`

Status: **Executed successfully from start to finish**

The notebook was run using the `Python 3.10 (ML4T Core)` Jupyter kernel.

## Compatibility Changes

### 1. Matplotlib 3D Axes Creation

#### Original code

```python
three_dee = plt.figure(figsize=(15, 5)).gca(projection="3d")
````

#### Modernized code

```python
fig = plt.figure(figsize=(15, 5))
three_dee = fig.add_subplot(1, 1, 1, projection="3d")
```

#### Reason

The installed Matplotlib version no longer accepts the `projection`
argument in `Figure.gca()`.

`Figure.add_subplot()` explicitly creates an axes object with the required
3D projection.

This change preserves the original plotting behavior.

---

### 2. scikit-learn `SGDRegressor` Loss Name

#### Original code

```python
sgd = SGDRegressor(
    loss="squared_loss",
    penalty="l2",
    fit_intercept=True,
)
```

#### Modernized code

```python
sgd = SGDRegressor(
    loss="squared_error",
    penalty="l2",
    fit_intercept=True,
)
```

#### Reason

Modern versions of scikit-learn use:

```python
loss="squared_error"
```

instead of the deprecated name:

```python
loss="squared_loss"
```

Both names refer to the ordinary squared-error regression objective, so this
change does not alter the mathematical meaning of the model.

---

### 3. Deprecated `n_iter` Reference

The original notebook contains the following commented line:

```python
# sgd.n_iter = np.ceil(10**6 / len(y))
```

This line remains commented out.

Modern versions of scikit-learn control the maximum number of training
iterations through the `max_iter` constructor parameter:

```python
sgd = SGDRegressor(
    loss="squared_error",
    max_iter=1000,
)
```

No change was required for the current notebook because the old `n_iter`
assignment was not executed.

## Validation Results

The following components completed successfully:

* Synthetic regression data generation
* NumPy mesh-grid construction
* pandas DataFrame creation
* Matplotlib 3D scatter plotting
* seaborn plotting utilities
* Ordinary least-squares regression
* statsmodels regression analysis
* scikit-learn linear regression
* Stochastic gradient descent regression
* Notebook execution from the first cell to the final cell

No external market data, API key, GPU, or additional data download was
required.

## Outcome

The notebook now runs successfully on the modern `ml4t-core` environment
with two necessary compatibility updates:

1. Replace `Figure.gca(projection="3d")` with
   `Figure.add_subplot(..., projection="3d")`.
2. Replace `SGDRegressor(loss="squared_loss")` with
   `SGDRegressor(loss="squared_error")`.

The original educational purpose, regression models, and mathematical
behavior of the notebook remain unchanged.



