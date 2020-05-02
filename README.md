# Final Project in Course: Deep learning 236781.
## Introduction:
Our work based on paper [Smoothed Inference for Improving Adversarial Robustness](https://arxiv.org/pdf/1911.07198.pdf).
Our mission is to implement more efficient voting functions which produce better results than the one that was suggested in the paper, we are improving the Monte Carlo algorithm implemented On Resnet20 with new voting functions. Link to the Paper Repo [Here](https://github.com/yanemcovsky/SIAM/tree/947630e7091e682cb827b568535ddf3e784a28ff).
## Our changes mainly was in these files:
- models/resnet_cpni_smoothed_predict.py: 
    here we implemented a new class that inherits from the original resnet class, ovrriden the Monte Carlo algorithm and used in it the voting functions that we implemented (which are implemented also in this file).
- train.py: adapt the train parameters to the new functions.
- run_attack.py: adapt the attack parameters to the new voting functions.

## Train and Attack commands:
note all the command should run from the SIAM directory.
### the format to run the train:
```sh
python train.py --weight-noise --cpni  --adv --epochs 50 --smooth mcpredict --<vote_function> <theshold_value> --attack pgd --schedule 200 300  --results_dir ./final_results
```
for example:
```sh
 python3 train.py --weight-noise --cpni  --adv --epochs 50 --smooth mcpredict --top2weighted 0.08 --attack pgd --schedule 200 300  --results_dir ./final_results
```
### our format to run the attack:
```sh
python3 run_attack.py --weight-noise --cpni --epochs 50 --smooth mcpredict --<voting_function> <threshold_value> --attack pgd --m_test 16 --m_train 16 --resume <path_to_model> > <path_to_att_output>
```
Example:
```sh
python3 run_attack.py --weight-noise --cpni --epochs 50 --smooth mcpredict --Voter_Weighted2 0.08 --attack pgd --m_test 16 --m_train 16 --resume ./final_results/final_results/Voter_weighted2/train_result/threshold_08/2020-05-01_11-21-07 > ./final_results/att_results/Voter_Weighted_0.08.txt

```
### voting_functions:
- top2threshold
- top2threshold_softmax
- Voting_Weighted2
- top2weighted
- top2weighted_softmax
- safe_pred

for more information about the implementations, you can refer to our report.