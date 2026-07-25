# Chapter 07 Modernization Notes

## Scope

This document records compatibility changes made to the following notebook:

- `01_linear_regression_intro.ipynb`

The goal is to run the original second-edition notebook on a modern Python
environment while preserving its original educational purpose, model
definitions, and numerical behavior.

## Runtime Environment

### Primary environment

The notebook was validated in the following environment:

- Environment: `ml4t-core312`
- Python: 3.12.13
- Python executable:
  `/home/qzhan054/miniforge3/envs/ml4t-core312/bin/python`
- NumPy: 1.26.4
- pandas: 2.2.3
- scikit-learn: 1.7.2
- Matplotlib: 3.10.9

The environment passed the following dependency check:

```text
No broken requirements found.
````

The notebook kernel is registered as:

```text
Python 3.12 (ML4T Core)
```

### Compatibility environment

The notebook was initially modernized and executed successfully using the
Python 3.10 `ml4t-core` environment.

The Python 3.10 environment is retained temporarily as a compatibility
fallback while additional notebooks are migrated to Python 3.12.

## Notebook Status

### `01_linear_regression_intro.ipynb`

Status: **Executed successfully from start to finish on Python 3.12.**

The notebook was validated using the `Python 3.12 (ML4T Core)` Jupyter
kernel.

All cells completed without exceptions after:

1. restarting the kernel;
2. running all cells from top to bottom;
3. saving the executed notebook.

## Compatibility Changes

### 1. First Matplotlib 3D Axes Creation

The original notebook creates a three-dimensional axes object using
`Figure.gca()`.

#### Original code

```python
three_dee = plt.figure(figsize=(15, 5)).gca(projection="3d")
```

#### Modernized code

```python
fig = plt.figure(figsize=(15, 5))

three_dee = fig.add_subplot(
    1,
    1,
    1,
    projection="3d",
)
```

#### Reason

The installed Matplotlib version no longer accepts the `projection`
argument through `Figure.gca()`.

`Figure.add_subplot()` explicitly creates an axes object with the requested
three-dimensional projection.

The arguments:

```python
1, 1, 1
```

mean:

* one row;
* one column;
* the first subplot.

This change preserves the original plotting behavior.

### 2. Second Matplotlib 3D Axes Creation

The notebook contains a second three-dimensional plot that used the same
deprecated API.

#### Original code

```python
three_dee = plt.figure(figsize=(15, 5)).gca(projection="3d")
```

#### Modernized code

```python
fig = plt.figure(figsize=(15, 5))

three_dee = fig.add_subplot(
    1,
    1,
    1,
    projection="3d",
)
```

#### Reason

The same Matplotlib compatibility issue applies to both three-dimensional
plots.

Both cells now use the same explicit and consistent axes-creation API.

### 3. scikit-learn `SGDRegressor` Loss Name

The original notebook uses the former name of the squared-error loss
function.

#### Original code

```python
sgd = SGDRegressor(
    loss="squared_loss",
    fit_intercept=True,
    shuffle=True,
)
```

#### Modernized code

```python
sgd = SGDRegressor(
    loss="squared_error",
    fit_intercept=True,
    shuffle=True,
)
```

#### Reason

Modern versions of scikit-learn use:

```python
loss="squared_error"
```

instead of:

```python
loss="squared_loss"
```

Both names represent the ordinary squared-error regression objective.

This is an API naming change and does not alter the mathematical objective
of the model.

### 4. Deprecated `n_iter` Reference

The original notebook contains the following commented line:

```python
# sgd.n_iter = np.ceil(10**6 / len(y))
```

The line remains commented out and is not executed.

Modern versions of scikit-learn control the maximum number of training
iterations through the `max_iter` constructor parameter:

```python
sgd = SGDRegressor(
    loss="squared_error",
    max_iter=1000,
)
```

No runtime change was required because the original `n_iter` assignment was
already disabled.

## Behavioral Preservation

The compatibility changes are limited to API migration:

1. Two calls to `Figure.gca(projection="3d")` were replaced with
   `Figure.add_subplot(..., projection="3d")`.
2. `SGDRegressor(loss="squared_loss")` was replaced with
   `SGDRegressor(loss="squared_error")`.

The following notebook behavior remains unchanged:

* Synthetic data-generation logic
* Linear-regression specification
* Regression target
* Model features
* Ordinary least-squares calculations
* Stochastic-gradient-descent objective
* Plot contents
* Statistical interpretation

No model parameters were intentionally tuned or altered as part of the
migration.

## Validation Procedure

The Python 3.12 validation procedure was:

1. Open `01_linear_regression_intro.ipynb`.
2. Select the `Python 3.12 (ML4T Core)` kernel.
3. Restart the Jupyter kernel.
4. Run all notebook cells from top to bottom.
5. Confirm that no cell produces an exception.
6. Confirm that the regression models fit successfully.
7. Confirm that both three-dimensional charts render successfully.
8. Save the executed notebook.
9. Review source changes with `nbdime`.

The source-only comparison command is:

```bash
cd ~/projects/machine-learning-for-trading

nbdiff --sources \
  origin/second-edition \
  07_linear_models/01_linear_regression_intro.ipynb
```

The expected source changes are:

* one Markdown cell documenting the modern environment;
* two Matplotlib 3D axes compatibility changes;
* one scikit-learn loss-name compatibility change.

## Validation Results

The following components completed successfully on Python 3.12:

* Synthetic regression data generation
* NumPy mesh-grid construction
* pandas DataFrame creation
* Matplotlib three-dimensional scatter plotting
* seaborn plotting utilities
* Ordinary least-squares regression
* statsmodels regression analysis
* scikit-learn linear regression
* Stochastic-gradient-descent regression
* Notebook execution from the first cell to the final cell
* Rendering of all notebook charts
* Import of all required dependencies
* `python -m pip check`

No notebook cell produced an exception during the final validation run.

## External Requirements

This notebook does not require:

* external market data;
* API credentials;
* a database;
* a GPU;
* CUDA;
* Zipline;
* Alphalens;
* Pyfolio;
* TensorFlow;
* PyTorch.

The notebook uses locally generated synthetic data.

## Outcome

`01_linear_regression_intro.ipynb` now executes successfully from start to
finish using Python 3.12.13 and the `ml4t-core312` environment.

The modernization required three source-code compatibility changes:

1. Two Matplotlib calls using
   `Figure.gca(projection="3d")` were replaced with
   `Figure.add_subplot(..., projection="3d")`.
2. The scikit-learn loss name `squared_loss` was replaced with
   `squared_error`.

These changes preserve the notebook's original:

* data-generation process;
* regression specifications;
* squared-error objective;
* visualizations;
* statistical interpretation;
* educational purpose.

The notebook is now validated on the project's primary Python 3.12
environment.

