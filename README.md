# Vector Quantized Contrastive Predictive Coding for Template-based Music Generation
Gaëtan Hadjeres, Sony CSL, Paris, France (gaetan.hadjeres@sony.com)\
Léopold Crestel, Sony CSL, Paris, France (leopold.crestel@sony.com)

This is the companion github of the paper 
[Vector Quantized Contrastive Predictive Coding for Template-based Music Generation](www.google.com).
In this paper, we proposed a flexible method for generating variations of discrete sequences 
in which tokens can be grouped into basic units, like sentences in a text or bars in music.
More precisely, given a template sequence, we aim at producing novel sequences sharing perceptible similarities 
with the original template without relying on any annotation.
We introduce 
 - a *self-supervised encoding* technique, named *Vector Quantized Contrastive Predictive Coding* (*VQCPC*), 
which allows to learn a meaningful assignment of the basic units over a discrete set of codes,
together with  mechanisms allowing to control the information content of these learnt discrete representations.
- a *decoder* architecture which can generate sequences from the compressed representations learned by the encoder.
In particular, it can be used to generate variations of a template sequence.
 
Our experiments on the corpus of J.S. Bach chorales can be reproduced using this repository.

** SCHEMA STYLE OU CA ENCODE ET CA DECODE, ON VOIT LE DOWNSAMPLING LOCAL DES TOKEN EN 1 SYMBOL DISCRET,
 ET LE UPSCALING (LOCAL AUSSI) DES CODES VERS UNE SEQUENCE; BÔTé GARANTIE** 


## Installation
To install
- clone the repository.
- run (we recommend using a virtualenv) 
        
        pip install -r requirements.txt

## How to use it
All the experiments reported here can be reproduced with the different configuration files located in VQCPCB/configs.

Encoders are trained independently from the decode, in a self-supervised manner.
To train a particular encoder, run the following command

    python main_encoder.py -t -c VQCPCB/configs/encoder_*.py

with encoder_* being the name of the configuration file. 

Trained models are stored in *models/*.
To observe the clusters learned by a trained encoder, you can run the command

    python main_encoder.py -l -c models/encoder_*/config.py
    
To train a decoder for a particular encoder, you can run

    python main_decoder.py -t -c VQCPCB/configs/decoder_*.py 
    
after having specified in the configuration file VQCPCB/configs/decoder_*.py the path to the encoder:

    'config_encoder':              'models/encoder_*/config.py',
    
Variations of chorales excerpts 
as well as the complete re-harmonisation of all the chorales found in our corpus can be generated by running

    python main_decoder.py -l -c models/decoder_*/config.py 

## Experiments
### Clusters
- Sounds
- 3D map
- few words about how the different methods lead to clustering based on different features

|       |  LSTM downscaler | Transformer downscaler  
| :--- |:---:| :---:
| Random | |
| Same sequence | |
| Student | X |
| Random and no quantization | |
| Same sequence and no quantization |  |
| Student and no quantization| X | 

### Template-based generation
QUOI MONTRER
- tests perceptifs
    Q = extrait préféré
    Q = lequel respecte le mieux la structure d'origine
- petits fragments original // 3 variations
- rewritting d'un chorale complet

Parameters encoder
- Negative sampling scheme + student
- Quantization bottleneck
- Type of downsampling

Decoding is done with a relative transformer (**DESCRIBED IN PAPER**)

**ON MET DES SAMPLES DANS LES CASES**

|       |  LSTM downscaler | Transformer downscaler  
| :--- |:---:| :---:
| Random | |
| Same sequence | |
| Student | X |
| Random and no quantization | |
| Same sequence and no quantization |  |
| Student and no quantization| X | 

Parameters decoder
- Attention masks AC//D//C ; F//F//C ; AC//AC//C
- relative_decoder VS standard transformer with positioning absolue absurde + pas de SRel

|       |  Transformer | Relative transformer  
| :--- |:---:| :---:
| Random |  | 
| Same sequence |  |
