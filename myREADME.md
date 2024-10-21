Progress
• Fixed dependencies issues by setting up an environment with python 3.7.7 and used that for all experiments.
• Was able to figure out whole folder/file structure and pipeline
• Was able to preprocess logs
• Preprocessed logs, generated graph and then through graph_reader.py generated sequence graph
• First had to generate sampled datasets by setting variables in atlas.py
• Then train using sampled datasets
• Then testing and evaluation
• Fixed syntax errors in multipreprocess and ran file successfully.


Issues
• Dot issue while parsing; got fixed using Jaffer’s files.
• Had to copy paste files from paper_experiments folder.
• Graph generation, sampling and training take the most time
• Difference in predicted entities.
• Getting 0 FPs and FNs on repeated attempts on my eval file but their eval showing some FPs.
• Syntax errors in multi hosting attacks and unclear file structure and their usage in paper_experiments folder. Not mentioned anything in readme.
• Python 2 syntax found in multi hosting files such as xrange, f.next() so had to replace with Python 3's.
• Code stuck for 1.5 hours after fixing graph generator in multi hosting.


Others
• Posted issue on gtithub regarding 0 FP and FN.
