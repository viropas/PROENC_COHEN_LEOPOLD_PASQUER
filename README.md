# Projet_Ifremer
This Github regroups a list of tools and tutorials for estimating a genome size. One can find examples and results in the dedicated sections. 

K-mer distribution is the first step leading to the estimation of the genome size.

To use the tools,one needs to input a k value and a corresponding k-mer histo file generated with short reads, which contains two tab-separated columns. The first column gives frequencies at which k-mers occur in reads, while the second column gives counts of such distinct k-mers (link histo file).

Given a fastq file, here is an example for counting k-mers with jellyfish:
```shell
jellyfish count -t 8 -C -m k -s 5G -o kmer_out --min-qual-char="?" path/to/fastq/file
```
k is the size of k-mers. Here are the options used in the counting k-mers:
```shell
-t    -treads=unit32       Number of treads to be used in the run. eg: 1,2,3,..etc.
-C    -both-strands        Count both strands
-m    -mer-len=unit32      Length of the k-mer    
-s    -size=unit32         Hash size / memory allocation  
-o    -output=string       Output file name
--min-quality-char         Base quality value. Version 2.2.3 of Jellyfish uses the “Phred” score, where "?" = 30
```
Then using the above created file (kmer_out), data points for a histogram will be created using the following command:
```shell
jellyfish histo -o kmer_out.histo kmer_out
```
This will generate the histo file needed to use the tools.
