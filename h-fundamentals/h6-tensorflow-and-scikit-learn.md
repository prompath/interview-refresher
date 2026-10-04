[Contents](../index.md) · H6 · P3

# TensorFlow and scikit-learn

## In one minute

scikit-learn is the standard library for classical machine learning; its strength is one
consistent interface (`fit`, `predict`, `transform`) and pipelines that keep preprocessing
inside cross-validation. TensorFlow, through its Keras API, is for neural networks: define
layers, compile with a loss and optimiser, and fit with callbacks.

## Key ideas

- **scikit-learn interface.** Estimators have `fit`; predictors add `predict` and
  `predict_proba`; transformers add `transform`.
- **Pipeline and ColumnTransformer.**

  ```python
  from sklearn.compose import ColumnTransformer
  from sklearn.pipeline import Pipeline
  from sklearn.preprocessing import OneHotEncoder, StandardScaler
  from sklearn.linear_model import LogisticRegression

  pre = ColumnTransformer([
      ("num", StandardScaler(), num_cols),
      ("cat", OneHotEncoder(handle_unknown="ignore"), cat_cols),
  ])
  model = Pipeline([("pre", pre), ("clf", LogisticRegression(max_iter=1000))])
  ```

  The whole pipeline is fitted inside each fold, which prevents leakage.
- **Model selection.** `cross_val_score`, `GridSearchCV`, `RandomizedSearchCV`; splitters
  `StratifiedKFold`, `GroupKFold`, `TimeSeriesSplit`.
- **Custom transformers.** A class with `fit` and `transform`, or `FunctionTransformer`.
- **Persistence.** `joblib`; pin the library version.
- **Keras model.**

  ```python
  import tensorflow as tf

  model = tf.keras.Sequential([
      tf.keras.layers.Input(shape=(n_features,)),
      tf.keras.layers.Dense(64, activation="relu"),
      tf.keras.layers.Dropout(0.2),
      tf.keras.layers.Dense(1),
  ])
  model.compile(optimizer="adam", loss="mse")
  model.fit(X, y, validation_split=0.2, epochs=100,
            callbacks=[tf.keras.callbacks.EarlyStopping(patience=10, restore_best_weights=True)])
  ```

- **Neural network basics.** Layers and activations (ReLU, sigmoid, softmax); loss;
  backpropagation computes gradients; optimisers (SGD, Adam); batch size, epochs,
  learning rate; overfitting controls (dropout, early stopping, weight decay); batch
  normalisation.
- **Keras APIs.** Sequential, functional (multiple inputs and outputs), subclassing.
- **`tf.data`.** Input pipelines with batching, shuffling and prefetching.
- **TensorFlow versus PyTorch.** PyTorch dominates research and much of industry now;
  the concepts transfer. Keras 3 runs on several backends.

## On my CV

scikit-learn and TensorFlow in Libraries. TensorFlow was used for one of the candidate
models in the load and solar forecasting work.

**To fill in (only I know):** whether I have used PyTorch, and how much.

## Likely questions

1. **Why use a Pipeline?** One object to fit and deploy, and no preprocessing leakage in
   cross-validation.
2. **Grid or random search?** Random covers more distinct values per parameter for the
   same budget.
3. **What does early stopping do?** Stops when validation loss stops improving and keeps
   the best weights.
4. **Do you know PyTorch?** Answer truthfully; the concepts are the same either way.
5. **Senior follow-up: when is a neural network the wrong tool?** Small tabular data,
   where boosted trees are stronger and cheaper.

## Pitfalls

- Overstating deep learning experience.

## Sources

- scikit-learn, pipelines and composite estimators: <https://scikit-learn.org/stable/modules/compose.html>
- Keras guides: <https://keras.io/guides/>
- TensorFlow tutorials: <https://www.tensorflow.org/tutorials>
