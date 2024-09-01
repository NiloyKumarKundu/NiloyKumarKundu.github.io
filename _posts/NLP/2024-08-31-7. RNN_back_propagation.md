---
title: '7\. RNN Back Propagation'
date: 2024-08-31
permalink: /posts/2024/08/recurrent-neural-network/
tags:
  - NLP
---

## Why Apply Backpropagation?

Backpropagation through time (BPTT) is the method used to compute these weight adjustments. BPTT calculates how the loss function changes with respect to each weight by applying the chain rule to propagate the gradients backward through the network's time steps.

After performing forward propagation in an RNN, we obtain an output \\(\hat{y}_i\\) for each time step, and we compute the loss function:

\\[ \text{loss} = (\hat{y}_i - y) \\]

where \\(\hat{y}_i\\) is the predicted output and \\(y\\) is the true value. The goal of training is to minimize this loss to make the model’s predictions as accurate as possible. To achieve this, we need to adjust the weights of the network.

## How Backpropagation Through Time Works

1. **Compute Derivative of the Loss Function:**

   To minimize the loss, we first need to compute the derivative of the loss function with respect to the predicted output \\(\hat{y}_i\\):

   \\[ \frac{\partial L}{\partial \hat{y}_i} \\]

   where \\(L\\) is the loss function. This derivative tells us how much the loss changes as \\(\hat{y}_i\\) changes.

2. **Update the Last Layer Weight (\\(w_3\\)):**

   The weight \\(w_3\\) in the last layer is directly connected to the output \\(\hat{y}_i\\). To find out how \\(w_3\\) affects the loss, we use the chain rule:

   \\[ \frac{\partial L}{\partial w_3} = \frac{\partial L}{\partial \hat{y}_i} \times \frac{\partial \hat{y}_i}{\partial w_3} \\]

   This derivative indicates how to adjust \\(w_3\\) to reduce the loss. We then subtract this value from \\(w_3\\) to update it:

   \\[ w_3 = w_3 - \eta \times \frac{\partial L}{\partial w_3} \\]

   where \\(\eta\\) is the learning rate.

3. **Update the Previous Layer Weights (\\(w_2\\)):**

   Next, we update \\(w_2\\). The output \\(o_4\\) at time step \\(t=4\\) depends on \\(w_2\\), and \\(\hat{y}_i\\) depends on \\(o_4\\). To update \\(w_2\\), we compute:

   \\[ \frac{\partial L}{\partial w_2} = \frac{\partial L}{\partial \hat{y}_i} \times \frac{\partial \hat{y}_i}{\partial o_4} \times \frac{\partial o_4}{\partial w_2} \\]

   Here, \\(\frac{\partial \hat{y}_i}{\partial o_4}\\) and \\(\frac{\partial o_4}{\\partial w_2}\\) represent how the output and the hidden state affect the loss, respectively. Update \\(w_2\\) in a similar manner:

   \\[ w_2 = w_2 - \eta \times \frac{\partial L}{\partial w_2} \\]

4. **Continue Updating Weights for All Time Steps:**

   The process continues for each weight through all time steps. Each weight \\(w\\) at previous layers is updated by considering how changes in weights affect the final loss. For instance, weights \\(w_1\\), \\(w\\), and \\(w_4\\) are updated in a similar manner.

   Specifically, for \\(w_1\\), we need to calculate:

   \\[ \frac{\partial L}{\partial w_1} = \frac{\partial L}{\partial \hat{y}_i} \times \frac{\partial \hat{y}_i}{\partial o_4} \times \frac{\partial o_4}{\partial o_3} \times \frac{\partial o_3}{\partial w_1} \\]

   And for \\(w\\):

   \\[ \frac{\partial L}{\partial w} = \frac{\partial L}{\partial \hat{y}_i} \times \frac{\partial \hat{y}_i}{\partial o_4} \times \frac{\partial o_4}{\partial o_3} \times \frac{\partial o_3}{\partial o_2} \times \frac{\partial o_2}{\partial w} \\]

   All these calculations use the same weight matrices across time steps (e.g., \\(w_1 = w_2 = w_3 = w_4\\)).

5. **Iterative Training:**

   This process of calculating gradients and updating weights is repeated for many iterations (epochs) until the model reaches optimal weights or a minimum loss. This iterative process helps in fine-tuning the model to make accurate predictions.

By preserving and updating the sequence information through time, RNNs can learn complex patterns and dependencies in sequential data, leading to improved performance in tasks like NLP and time series prediction.
