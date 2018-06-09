# A Corpus of Grand National Assembly of Turkish Parliament's Transcripts

This repository contains the source code to create the corpus of transcriptions of 
Turkish parliament's general assembly.

We also provide the most recent version of the corpus at 
[Releases](https://github.com/onurgu/turkish-parliament-texts/releases) section.

## Contributing

If you want to contribute, you can follow these simple steps to create a development
environment:

    git clone https://github.com/onurgu/turkish-parliament-texts/releases
    
    wget http://voltran.cmpe.boun.edu.tr/temporary_download/datasets/tbmm/corpus-dev.tar.gz
    tar -zxvf corpus-dev.tar.gz
    
    pip3 install pipenv
    pipenv install --python 3
    
### Building the corpus

    nohup python -m corpus_compiler.builder --command construct_corpus --corpus_filename corpus-v0.4b/tbmm_corpus.mm --train_lda --vocabulary_filename corpus-v0.4b/vocabulary >> construct_vocab.nohup &
    
### Using the Jupyter notebook

You can use the `notebook.ipynb` file to load and query the corpus.

Example code to save a figure (using the small development corpus):
   
    pipenv shell
    ipython
    import corpus_loader
    
    corpus = corpus_loader.load(corpus_filepath="./corpus-dev/tbmm_corpus.mm")
    
    lda, topic_dist_matrix, label_vector = corpus_loader.load_lda_model(corpus, "./corpus-dev/tbmm_corpus.mm.tbmm_lda.model")
    
    # plot distribution of "mebus" and "milletvekil" keywords
    corpus_loader.corpus.plot_word_freqs_given_a_regexp_for_each_year([r"^mebus",r"^milletvekil"], ["mebus", "milletvekili"], keyword="milletvekil_and_mebus",)
    
    # to see plotted values 
    plot_values, counts, total_count, all_keywords = corpus_loader.corpus._word_freqs_given_a_regexp_for_each_year(r"^(milletvekil|vekil)", keyword="milletvekil",)
   
    
![notebook image](notebook.png)