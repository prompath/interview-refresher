[Contents](../index.md) · G5 · P2

# Deep learning forecasters

## In one minute

Neural forecasters learn from windows of past values directly. An LSTM reads the window
step by step, keeping a memory that gates decide to update or forget. They pay off with
many related series, long histories and complex inputs; on a single moderate series,
gradient boosting or a classical model is usually as accurate and far cheaper to train
and maintain.

## Key ideas

- **Recurrent networks.** A hidden state updated at each time step. Plain RNNs lose
  long-range information because gradients vanish.
- **LSTM.** Adds a cell state and three gates:
  - *forget*: what to drop from memory;
  - *input*: what new information to store;
  - *output*: what to expose as the hidden state.
  GRU is a lighter variant with two gates.
- **Input shape (Keras).** `(samples, timesteps, features)`. Each sample is a window.

  ```python
  model = tf.keras.Sequential([
      tf.keras.layers.Input(shape=(window, n_features)),
      tf.keras.layers.LSTM(64),
      tf.keras.layers.Dense(horizon),
  ])
  model.compile(optimizer="adam", loss="mae")
  ```

- **Multi-step output.** A dense layer with one unit per horizon step, or an
  encoder-decoder (sequence-to-sequence) where a decoder unrolls the forecast.
- **Preparation.** Scale inputs (fit the scaler on training data only); windowing;
  time-ordered train, validation and test.
- **Training controls.** Early stopping on validation loss, dropout, learning rate
  schedule, fixed seeds for repeatability.
- **Other architectures by name.** 1-D convolutions and temporal convolutional networks;
  DeepAR (probabilistic, global); N-BEATS and N-HiTS; Temporal Fusion Transformer;
  pretrained foundation models for time series (Chronos, TimesFM, TimeGPT) that forecast
  with no training on the target series.
- **When deep learning wins.** Many series trained together, rich covariates, long
  seasonal patterns, need for probabilistic output.
- **When it does not.** Short or single series. In the M5 forecasting competition the
  winning methods were gradient boosted trees, not neural networks.
- **Costs.** Tuning effort, training time, GPU, less interpretability, harder debugging.

## On my CV

TensorFlow is in Libraries because a TensorFlow model was one of the candidates in the
electric load and solar forecasting work.

**To fill in (only I know):** which architecture it was, and how it compared with the
other candidates.

## Likely questions

1. **How does an LSTM remember?** Through the cell state, changed only by the gated
   updates.
2. **Did the neural model beat boosting?** Give the real result and why.
3. **How do you prevent overfitting?** Early stopping, dropout, a simpler network, more
   series.
4. **What is the input shape and how do you build it?** Windows of timesteps × features.
5. **Senior follow-up: would you deploy the neural model if it is 1% better?** Usually
   not; weigh the gain against maintenance and retraining cost.

## Pitfalls

- Scaling with statistics from the full series.
- Comparing a tuned network against an untuned baseline.

## Sources

- TensorFlow, time series forecasting tutorial: <https://www.tensorflow.org/tutorials/structured_data/time_series>
- Olah, "Understanding LSTM Networks": <https://colah.github.io/posts/2015-08-Understanding-LSTMs/>
- Makridakis et al., "M5 accuracy competition: Results, findings, and conclusions": <https://www.sciencedirect.com/science/article/pii/S0169207021001874>
