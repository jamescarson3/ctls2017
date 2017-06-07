# Life Sciences Workflows

## Automating workflows 2

At this point, you should have a `blastp_workflow.sh` script that looks similar to the following:

```
#!/bin/bash

echo "workflow started at $(date)"

# validate and preprocess our input file(s)
if [[ $# -eq 1 ]]; then
	query="$1"
else
	echo "Please specify the query file as a command line argument"
    echo "Usage: blastp_workflow.sh query.pep"
    exit 1
fi

database="/work/01114/jfonner/public/ctls2017/refseq_protein/refseq_protein"


# run blastp
blastp -num_threads 12 -query $query -db $database


# postprocess our results

echo "workflow finished at $(date)"
```

At this point, we should also have a time estimate on how long we need to run our dataset.

- How long did it take to run blastp on `first10.pep`?
- How many sequences are in the full `query.pep`?
- If we do nothing different, how long would we estimate we need to run the full dataset?

### Data parallelism

The `blastp` command can use multiple threads, but (spoiler alert) the scaling is not all that great.  In the Optimization and Parallelization session this afternoon, you will learn how to test and quantify this.  For now, let's purse the strategy of splitting up our file and running independent blastp commands.

Splitting up a fasta file is a common task, and as such, we've already provided a script that does it called `splitfasta.pl`.  You most likely copied it to your local directory at the beginning of this session.  If not, it is availabe at `/work/01114/jfonner/public/ctls2017/splitfasta.pl`.

If we wanted to take our `first10.pep` file and split into individual reads, it would look something like this:

```
mkdir split_files
./splitfasta.pl -s first10.pep -f first10.pep -r 1 -o split_files
```

Note what the filenames are called now!

Now we could automate this in our script. **Put the splitfasta.pl command in your bash script**

Finally, to run independent blastp commands on each smaller file, we can use a bash `for` loop like the following:

```
for file in ./split_files/*; do
    blastp -num_threads 1 -query $file -db $database &
done
```

We have looked at for loops before.  At this point, let's take some time to work with this hands on and try running our script in parallel.

### Hands-On

Update your blasp_workflow.sh script to run an independent blastp command for each input file.

What are the limitations for how many reads you can accommodate?

Can you use the `grep` command in combination with an `if` statement to check if there are too many sequences in the query file?

Before you finish, be sure to clean up your directories, remove temporary files, and leave notes in your README file.

### Conclusion

There are lots of other improvements we could make, and a few we **should** make for our script.  In the hand-on time this afternoon, we can revisit this script and add `launcher` to make it work much better!


Previous: [Automating Workflows 1](workflows1_2.md) | Next: [Agenda](../../index.md)