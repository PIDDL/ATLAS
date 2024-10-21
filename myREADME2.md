## Progress after Meeting on 16-10-24

- Ran training on their resampled dataset and tested with their preprocessed testing sequence graph and preprocessed logs, still getting 0 FPs and 0 FNs.
- Now using their trained model with the same files for testing.
- Still getting 0 FPs and 0 FNs.
- Their evaluation file is showing fewer predicted entities compared to mine, and mine has higher probabilities for predicted entities when I ran `evaluate.py`, meaning my model is much more accurate.
- Next step is to reproduce their paper experiments (experiment S3 for now) to see if any changes occur in the evaluation file, training, testing, and evaluation.
