# Hash Cracking

### Wordlist Generation

Some tools to generate wordlists which can be used with hydra, john, etc

* #### Crunch

***

### Rainbow Tables (RainbowCrack)

* It is a table of hashes which is encoded by a particular algorithm e.g base64.
* Hash table are a hash of each word stored in a table
* Used for offline attacks only

#### rtgen

Used to generate rainbow tables. It has syntax

```bash
rtgen hash_algorithm charset plaintext_len_min plaintext_len_max table_index chain_len chain_num part_index
```

* Charset is character possibilities
* Table index is used to select reduction function
* Used to store large rainbow tables into smaller chunks

#### rtsort

Used to sort the rainbow table

#### rcrack

Used to crack the hash using rainbow table

***
