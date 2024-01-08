# Reverse-English
This repo was used to fine-tune the T5 model with Hugging Face to map English to Reverse English.

## Procedure
To fine-tune the T5 model with Hugging Face to map English to Reverse English, I took inspiration from Hugging Face's T5 fine-tuning [notebook](https://colab.research.google.com/github/NielsRogge/Transformers-Tutorials/blob/master/T5/Fine_tune_CodeT5_for_generating_docstrings_from_Ruby_code.ipynb#scrollTo=spbNHeE5ETpG)
\\
First, I interpreted Reverse English to be the reverse of a string. For example, an input of "hello" would map to "olleh", and "this is a ball" would map to "llab a si siht". Using this interpretation, I constructed a dataset that would contain text and reverse-text pairs. I used "ag-news" as the base dataset, and reversed all of the entries to create the pairs. From there, I trained the "t5-small" model, due to resource limitations, on the data using a pytorch lightning module. Since the model was trained on colab, the training took place over eight different training instances - that is, the training was stopped and restarted eight times. This was done due to idle timeout issues. In total, the model was trained for 40 epochs.

## Results
Below is the training loss observed in the last 10 epochs. The training loss experienced a gradual decrease and didn't fully plateau.
\\
Below is the validation loss observed in the last 10 epochs. The validation loss also didn't plateau and continued to steadily decrease, indicating that the drop in training loss was not due to overfitting. I could have continued training the model as the loss was continuing to drop, but I chose to terminate the training here due to time and resource limitations.
\\
The above images were taken from TensorBoard logs.
\\
Some sample input output pairs are shown below:
**Test:** `Fears for T N pension after talks Unions representing workers at Turner   Newall say they are 'disappointed' after talks with stricken parent firm Federal Mogul.`
**Reversed Sentence:** `.lugoM laredeF mrif tnerap nekcirts htiw sklat retfa 'detnioppasid' era yeht yas llaweN rehtorT ta srekrow gnitneserper snoinU sklat retfa noisnep N T rof sraeF`

**Test:** `Ky. Company Wins Grant to Study Peptides (AP) AP - A company founded by a chemistry researcher at the University of Louisville won a grant to develop a method of producing better peptides, which are short chains of amino acids, the building blocks of proteins.`
**Reversed Sentence:** `.seiroloc fo skcolb gnidliub eht,seirolocinam fo sniahc trohs era hcihw,seiroloc retteb gnicudorp fo yhtem a poleved ot tnarg a now ellivskcuL fo ytisrevinU eht ta rehcraeser ygolonhcet a yb dednuof ynapmoc A - PA )PA( sedeptiP ydutS ot tnarG sniW ynapmoC.yK`

## Navigating Repo
Everything to do with training the model and inference are the in model_training.ipynb, which is the downloaded Google Colab notebook. The training logs can be found in the lightning_logs directory. Finally, the predictions made on the test set can be found in inferences.csv.
