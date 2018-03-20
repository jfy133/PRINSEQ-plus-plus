![Prinseq++](prinseq_logo.png)

PRINSEQ++ is a C++ implementation of the prinseq-lite.pl program. It can be used to filter, reformat or trim genomic and metagenomic sequence data. It is 5X faster than prinseq-lite.pl and uses less RAM thanks to the use of multi-threading and the cboost libraries. It can read and write compressed (gzip) files, drastically reducing the use of hard drive.

## Requierments
1. automake
2. g++
3. make
4. boost-devel
5. pthread

## Download
If you are just interested in compiling and using PRINSEQ++, download the latest [version](https://github.com/Adrian-Cantu/PRINSEQ-plus-plus/releases/download/v1.0/prinseq++-1.0.tar.gz).
If you want to edit the source code, clone this repository

## To install
1. tar -xvf pprinseqc-0.9.1.tar.gz
2. cd pprinseqc-0.9.1
3. ./configure
4. make
4. sudo make install

## To use the repository
1. ./autogen.sh
2. ./configure
3. make
4. make test 


## Usage

Option:
    -h | -help
        Print the help page; ignore other arguments.
        
    -v | -version
        Print version; ignore other arguments.
        
    -threads 
        Nuber of threads to use. Note that if more than one thread is used, output
        sequences might not be in the same order as input sequences. (Default=1)
    
    ***** INPUT OPTIONS *****
    
    -fastq <file>
        Input file in FASTQ format. Can also read a compressed (.gz) file.
        
    -fastq2 <file>
        Input file in FASTQ format for pair-end reads. Can also read a 
        compressed (.gz) file.
        
    
    ***** OUTPUT OPTION *****
    
    -out_format <int>
        Set output format. 0 FASTQ, 1 FASTA. (Default=0)
        
    -out_name <string>
        For pair-end sequences, the output files are <string>_good_out_R1 and
        <string>_good_out_R2 for pairs where both reads pass quality control,
        <string>_single_out_R1 and <string>_single_out_R2 for read that passed
        quality control but mate didn't. <string>_bad_out_R1 and <string>_bad_out_R2  
        for reads that fail quality controls. [Default = random size 6 string] 
    
    -rm_header
        Remove the header in the 3rd line of the fastq (+header -> +). This does
        not change the header in the 1st line (@header).
        
    -out_gz 
        Write the output to a compressed file (WARNING this can be really SLOW)
        
    ***** FILTER OPTION ******
        
    -min_len <int>
        Filter sequence shorter than min_len.
    
    -max_len <int>
        Filter sequence longer than max_len.
        
    -min_gc <float>
        Filter sequence with GC percent content below min_gc.
    
    -max_gc <float>
        Filter sequence with GC percent content above min_gc.
    
    -min_qual_score <int>
        Filter sequence with at least one base with quality score below 
        min_qual_score.
        
    -min_qual_mean <int>
        Filter sequence with quality score mean below min_qual_mean.
        
    -ns_max_n <int>
        Filter sequence with more than ns_max_n Ns.
   
    -noiupac         
        Filter sequence with characters other than A, C, G, T or N.

    -derep
        Filter duplicated sequences. This only remove exact duplicates.
        
    -lc_entropy=[float]
        Filter sequences with entropy lower than [float]. [float] should be in
        the 0-1 interval. (Default=0.5)

    -lc_dust=[float]
        Filter sequences with dust_score lower than [float]. [float] should be in
        the 0-1 interval. (Default=0.5)
        
    ***** TRIM OPTIONS *****

    -trim_tail_left <integer>
        Trim poly-A/T tail with a minimum length of <integer> at the
        5'-end.

    -trim_tail_right <integer>
        Trim poly-A/T tail with a minimum length of <integer> at the
        3'-end.

    -trim_qual_rule <string>
        Rule to use to compare quality score to calculated value. Allowed
        options are lt (less than), gt (greater than) and et (equal to).
        [default: lt]

    -trim_qual_left=[float]
        Trim recursively from the 3'-end chunks of length -trim_qual_step if the
        mean quality of the first -trim_qual_window bases is less than [float]. 
        (Default=20)
        
    -trim_qual_right=[float]
        Trim recursively from the 5'-end chunks of length -trim_qual_step if the
        mean quality of the last -trim_qual_window bases is less than [float]. 
        (Default=20)    

    -trim_qual_window [int]
        Size of the window used by trim_qual_left and trim_qual_right (Default=5)

    -trim_qual_step [int]
        Step size used by trim_qual_left and trim_qual_right (Default=2)
    
    -trim_qual_type <string>
        Type of quality score calculation to use. Allowed options are min,
        mean, max and sum. [default= min]
