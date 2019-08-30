# Compact Language Detector v3 (CLD3) Python Edition

* [Model](#model)
* [Installation](#installation)
* [Contact](#contact)
* [Credits](#credits)

### Notes
This is an effort to fix issues with the initial Python fork at https://github.com/Elizafox/cld3
including memory leaks and no reuse of a Language model for multiple calls. This also pulls in much newer cld3 upstream code.


### Model

CLD3 is a neural network model for language identification. This package
 contains the inference code and a trained model. The inference code
 extracts character ngrams from the input text and computes the fraction
 of times each of them appears. For example, as shown in the figure below,
 if the input text is "banana", then one of the extracted trigrams is "ana"
 and the corresponding fraction is 2/4. The ngrams are hashed down to an id
 within a small range, and each id is represented by a dense embedding vector
 estimated during training.

The model averages the embeddings corresponding to each ngram type according
 to the fractions, and the averaged embeddings are concatenated to produce
 the embedding layer. The remaining components of the network are a hidden
 (Rectified linear) layer and a softmax layer.

To get a language prediction for the input text, we simply perform a forward
 pass through the network.

![Figure](model.png "CLD3")

### Installation
Building the Python wheel requires the protobuf compiler and its headers to be installed.
If you run into issues with protobufs not compiling, just go into the `src` directory and run

```
mkdir -p cld_3/protos
protoc --cpp_out=cld_3/protos *.proto
```

To generate a python wheel (from the root of this repo):

```
python setup.py bdist_wheel
```

Builds have been tested with GCC9.0 on Ubuntu 18.04 and Apple Clang 11.0.0 on OSX 10.15 (Catalina Beta)

### Credits

Original authors of the code in this package include (in alphabetical order):

* Alex Salcianu
* Andy Golding
* Anton Bakalov
* Chris Alberti
* Daniel Andor
* David Weiss
* Emily Pitler
* Greg Coppola
* Jason Riesa
* Kuzman Ganchev
* Michael Ringgaard
* Nan Hua
* Ryan McDonald
* Slav Petrov
* Stefan Istrate
* Terry Koo

and Elizabeth Myers for the original Python bindings
