## Progress after Meeting on 16-10-24

- Ran training on their resampled dataset and tested with their preprocessed testing sequence graph and preprocessed logs, still getting 0 FPs and 0 FNs.
- Now using their trained model with the same files for testing.
- Still getting 0 FPs and 0 FNs.


- Their evaluation file is showing fewer predicted entities compared to mine, and mine has higher probabilities for predicted entities when I ran `evaluate.py`, meaning my model is much more accurate.


- Their predicted:

![- their predicted:](images/their%20predicted%20S3.png)


- My predicted:

![- my predicted:](images/my%20predicted.png)


- file size for resampled dataset for me is different than theirs and their my training time less as compared to theirs

- Their resampled dataset:

![- their predicted:](images/their%20resampled.png)


- My resampled dataset: 

![- my predicted:](images/my%20resampled.png


- Next step is to reproduce their paper experiments (experiment S3 for now) to see if any changes occur in the evaluation file, training, testing, and evaluation.
