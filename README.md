![alt text]([http://url/to/img.png](https://github.com/activating-ai/IceCube-Neutrinos-in-Deep-Ice/blob/main/neutrino.png))


Abstract [what]

gpt is mainly for language model to predict next word(s) in sequence. however, this notebook (and other very early open notebooks, see [appendix] ) shows the [datasets] from the iceCube Neutrino Observatory may contain language-like [structures], after using gpt to predict neutrino particle’s direction.


Introduction [why]

The main use case for gpt-based models is known for [language] related datasets. for instance, text and images, these are language related, and the [known true] is that, there are some [logics] or [intelligent] inside of human text, human created images. however, in this notebook (and other very early open notebooks, see [appendix] ), shows that non-language-related dataset from iceCube Neutrino Observatory, can be predicted in next sequence just like the [lauguage] can be predicted from gpt based model for the [next word], and because of:

consistency of how prediction pattern of reaching to [0.0] angular-dist-score from multiple different datasets (see train-test-split).
the nature of gpt is unsupervised learning.
total of 688898 characters, size of unique chars 12, actual unique chars [' ', '.', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0']
small number of iterations, the model shows strong prediction ability, which also means, less weights needed, and most importanly, it means some more strong NON-weight related [logics] or [intelligent] in the struture, similar to language.

leads to reverse prediction of a dataset may have [language] struture inside.
methods [how]
define input context
X_train_sample_df['text'] = ' ' + X_train_sample_df['event_id'].astype(str) + ' ' + X_train_sample_df['charge_sc'].astype(str) + ' ' + X_train_sample_df['auxiliary_num'].astype(str) + ' ' + X_train_sample_df['time_sc'].astype(str) + ' ' + X_train_sample_df['x_sc'].astype(str) + ' ' + X_train_sample_df['y_sc'].astype(str) + ' ' + X_train_sample_df['z_sc'].astype(str) + ' ' + X_train_sample_df['azimuth_sc'].astype(str) + ' ' + X_train_sample_df['zenith_sc'].astype(str) + ' '
configure the model parameters
create an model training injection callback function
load data from different batch files
create a gpt based model
feed input context into model trainer
monitoring loss and prediction result (angular_dist_score) from callback during the trainer run
run 6300[production] iters
batch files from [ 1, 60, 111, 240, 222, 389, 433, 555, 618 ]
9000[production] rows of data
test data from train-test split
results
from this notebook's prediction output, it shows it can start to making relative reasonable prediction about neutrino particle’s direction after 1350 iterations, the prediction output become consistent after 1700 iterations.

iter_dt 71.12ms; iter 1350: train loss 0.56368 input_context 778000508 0.388702 0 , reversed 0.9249987306885454 output_context: 778000508 0.388702 0 0.473239 0.443972 0.432305 0.474399 0.482462 0.286377 719430412 target event_id: 778000508
target azimuth: 0.482462, zenith: 0.286377


predicted azimuth: 0.482462, zenith: 0.286377
predict_zenith_reverse 0.7540110701466416, redict_azimuth_reverse 3.3472593432077193 check if both are float True angular_dist_score(az_true, zen_true, az_pred, zen_pred)3.3472593432077193, 0.7540110701466416, 3.3472593432077193, 0.7540110701466416
progress_rec {'iter_id': 1350, 'target_event_id': 778000508, 'target_azimuth': 0.482462, 'target_zenith': 0.286377, 'reverse target_azimuth': 3.3472593432077193, 'reverse target_zenith': 0.7540110701466416, 'predict_azimuth': '0.482462', 'predict_zenith': '0.286377', 'reverse_predict_charge': 0.9249987306885454, 'reverse_predict_azimuth': 3.3472593432077193, 'reverse_predict_zenith': 0.7540110701466416, 'score': 0.0}
[more] in the log shows the prediction patterns

Todo

get data from this paper

https://www.nature.com/articles/s41586-023-06202-5.epdf?sharing_token=4QiTJHLmMXCmsVaUG81FstRgN0jAjWel9jnR3ZoTv0ME6fH1aRaoPODpQzkjnuHIAzE7P-opql98g_HHC0IVuGvK4GUn5rfIRYpu3DKJz0C7-Rdpcg1S7J2gGhEF8NIVg5slVuFbhyfpcpRyRYu-FNRUbC6zPbh9POGPi5dnnmeOc48OLJzk80jXgHdU1WCBQXq_H2cBt8pAXlOZgNUekZKj5xMlJHj48xWzooJbbFKEfNd35Re3HP37kKqnh5CJOqAdD-kWwjw1eh4rTPbhJWmiuNSPTyRcb-J28gw9BhwRT4psAUKk4cZ1xYJrgPSqL95iOUaNRfLPLC8bJyvPYvJ4qalWVaDd9fHksLLMoYw%3D&tracking_referrer=www.huffingtonpost.co.uk

then test against these data, see what happans

Appendix

IceCube - Neutrinos in Deep Ice Reconstruct the direction of neutrinos from the Universe to the South Pole https://www.kaggle.com/competitions/icecube-neutrinos-in-deep-ice
minGPT https://github.com/karpathy/minGPT
first published notebook for showing the result https://www.kaggle.com/code/tyeestudio/gpt-based-prediction-no-chatgpt
then, watch it learn in this notebook https://www.kaggle.com/code/tyeestudio/gpt-based-prediction-watch-it-learn
show with liveplot https://www.kaggle.com/code/tyeestudio/gpt-based-prediction-live-loss-plot
note
this is an copy from my private notebook which has 77 versions.
because of each prediction takes about 0.3 seconds, this notebook timeout the submission
