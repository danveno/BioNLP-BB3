# BioNLP-BB3

BioNLP 2016 BB3 Contest Submission (http://2016.bionlp-st.org/tasks/bb2)


## Authors

Helen Cook [1], Evangelos Pafilis [2], Lars Juhl Jensen [1]

[1] Novo Nordisk Foundation Center for Protein Research, University of Copenhagen

[2] Institute of Marine Biology Biotechnology and Aquaculture, Hellenic Centre for Marine Research (HCMR)




## License

Code distributed under a BSD license, see LICENSE for details.
Dictionaries and output distributed under CC-BY 4.0.



## Manifest

This distribution contains the following files:

* tagger/BioNLP2016.py -- Python wrapper which is the main executable for the contest.  Reads contest formatted txt files, and writes .a1 and .a2 files.
* tagger/t-BioNLP2016.py -- Small test suite for the Python code
* tagger/tagger.py -- Swig-based library to interface with the C++ tagger
* tagger/tagger_swig.i
* tagger/chkcoord.py -- Small script to verify that the coordinates of manual annotated a1 files give the correct strings when referenced against the .txt input
* tagger/__init__.py
* tagger/tagger.cxx -- C++ tagger
* tagger/tagger_core.h
* tagger/acronyms.h
* tagger/tagger.h
* tagger/tokens.h
* tagger/tagger_types.h
* tagger/hash.h
* tagger/file.h
* tagger/tightvector.h
* tagger/Makefile
* tagger/LICENSE
* README -- this file



## Input Documents

Download the Entity Categorization training and development files located at http://2016.bionlp-st.org/tasks/bb2
and extract them into the documents directory.



## Input Dictionaries

A dictionary is provided for bacteria.  

* dict/bacteria_names.tsv
* dict/bacteria_entities.tsv
* dict/bacteria_stopwords.tsv
* dict/bacteria_groups.tsv
* dict/bacteria_genus

A dictionary is now also provided for habitats.  

* dict/habitat_names.tsv
* dict/habitat_entities.tsv
* dict/habitat_stopwords.tsv

All the dictionary files are shipped gzipped.


## Output

Under documents, this distribution also contains the precalculated output files for BioNLP BB3 Entity categorization training and dev sets.

* documents/*/*.a1.a2 predicted output

* documents/*/*.FN False negatives, according to manual annotations
* documents/*/*.FP False positives
* documents/*/*.OL Overlaps -- these would be true positives if the boundaries didn't matter, otherwise each counts as one false negative and one false positive
* documents/*/*.NM Normalization errors -- these would be true positives if the normalization didn't matter, otherwise each counts as one false negative and one false positive
* documents/*/*.TP True positives


## Install 

This code is known to compile under Suse Linux.  If you are compiling under another distribution of linux, you may need to install and configure the following libraries (beyond the scope of this document).
- swig
- boost

This code is known not to not compile out of the box on Mac OS X, but it is rumoured to be possible to do so with some code changes regarding the tr1 library.  Instructions and warranty not provided. 


## Usage

Run the tagger on a directory of files:

python tagger/BioNLP2016.py -f documents/BioNLP-ST-2016_BB-cat+ner_dev/*.a1 -e dict/bacteria_entities.tsv -n dict/bacteria_names.tsv -g dict/bacteria_stopwords.tsv -r dict/bacteria_groups.tsv -b dict/bacteria_genus -u -a dict/habitat_entities.tsv -o dict/habitat_names.tsv -s dict/habitat_global.tsv

This will write the output files described above.

To disable evaluation, remove the -u switch. 


Run the test suite:

python tagger/t-BioNLP2016.py

All 84 tests are expected to pass.

