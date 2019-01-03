1. Function introduction:
kmerfreq count K-mer (with size K) frequency from the input sequence data, typically sequencing reads data, and reference genome data is also applicable. The forward and reverse strand of a k-mer are taken as the same k-mer, and only the kmer strand with smaller bit-value is used to represent the kmer. It adopts a 16-bit integer with max value 65535 to store the frequency value of a unique K-mer, and any K-mer with frequency larger than 65535 will be recorded as 65535. The program store all kmer frequency values in a 4^K size array of 16-bit integer (2 bytes), using the k-mer bit-value as index, so the total memory usage is 2* 4^K bytes. For K-mer size 15, 16, 17, 18, 19, it will consume constant 2G, 8G 32G 128G 512G memory, respectively. kmerfreq works in a highly simple and parallel style, to achieve as fast speed as possible.  

2. Input and output:
Input is a library file that contains the path of all the input sequence files in fastq format or one-line fasta format��?with each line represents the path of a single sequence file. The program parse each sequencing reads file by the given order, and make a whole statistics. Output by default is a table file for the distribution of the kmer frequency, which can be analyzed for estimating sequencing quality and genomic characteristics. Two other optional output files are also avialable. By setting parameter "-w 1", the Kmer sequence with corresponding frequency values will be output for those K-mers with frequency value >= cutoff set by parameter -c; This is a human readable file that can facilate other kmer associated analysis. By setting parameter "-m 1", the whole kmer frequency table from the computer memory will be compressed and output, using 1-bit for each unique kmer, with 0 for kmer with frequency lower than cutoff set by parameter -q, and 1 for other kmers. This is a binary file, which can be reloaded to memory by other program that uses the kmer frequency data as input.

3. Command examples:
    (1) run with all default parameters
	kmerfreq  reads_files.lib
    (2) set basic parameters for statistics of kmer frequency 
	kmerfreq  -k 17 -t 10 -p Ecoli_K17 reads_files.lib
    (3) also output kmer sequence and frequency value with a cutoff
	kmerfreq  -k 17 -t 10 -p Ecoli_K17 -w 1 -c 5 reads_files.lib
    (4) also output the memory data of kmer frequency with a cutoff
	kmerfreq  -k 17 -t 10 -p Ecoli_K17 -m 1 -q 5 reads_files.lib

4. Reference papers:
A paper describing how to decide the kmer size for various data set and the potential applications for kmers:
Binghang Liu, Yujian Shi, Jianying Yuan, et al. and Wei Fan*. Estimation of genomic characteristics by analyzing k-mer frequency in de novo genome project. arXiv.org arXiv: 1308.2012. (2013)


