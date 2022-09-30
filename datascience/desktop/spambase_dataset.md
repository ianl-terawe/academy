# Acquire and Cleanse Data 

In this walkthrough, we analyze the spambase dataset. Spambase is a set of emails that are marked either spam or ham (not spam). Spambase also contains some statistics about the content of the emails. We talk about the statistics later in the walkthrough. 

## Download the spambase dataset 

The spambase dataset is a relatively small set of data that contains 4,601 examples. The dataset is a convenient size for demonstrating some of the key features of the DSVM because it keeps the resource requirements modest. 

<!--- VM size OK? --->

If you need more storage space, you can create additional disks and attach them to your DSVM. The disks use persistent Azure storage, so their data is preserved even if the server is reprovisioned due to resizing or is shut down. To add a disk and attach it to your DSVM, complete the steps in Add a disk to a Linux VM. The steps for adding a disk use the Azure CLI, which is already installed on the DSVM. You can complete the steps entirely from the DSVM itself. Another option to increase storage is to use Azure Files. 

To download the data, open a terminal window, and then run this command: 

```bash
wget --no-check-certificate https://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data 
```

The downloaded file doesn't have a header row. Let's create another file that does have a header. Run this command to create a file with the appropriate headers: 

```bash
echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers 
```

Then, concatenate the two files together: 

```bash
cat spambase.data >> headers 
mv headers spambaseHeaders.data 
```

The dataset has several types of statistics for each email: 

- Columns like `word_freq_WORD` indicate the percentage of words in the email that match `WORD`. For example, if `word_freq_make` is 1, then 1% of all words in the email were make 
- Columns like `char_freq_CHAR` indicate the percentage of all characters in the email that are `CHAR`
- `capital_run_length_longest` is the longest length of a sequence of capital letters
- `capital_run_length_average` is the average length of all sequences of capital letters
- `capital_run_length_total` is the total length of all sequences of capital letters
- `spam` indicates whether the email was considered spam or not (1 = spam, 0 = not spam)