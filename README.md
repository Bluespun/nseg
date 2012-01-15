Node.js Version of MMSG for Chinese Word Segmentation
======================================================
[![Build Status](https://secure.travis-ci.org/mountain/nseg.png)](http://travis-ci.org/mountain/nseg)

MMSG originally invented by Chih-Hao Tsai is a very popular Chinese word
segmentation algorithm. Many implementations are available on different
platforms including Python, Java, etc.

This package provide Node.js version of MMSG algorithm.

So far this package is still in developing, but the basic functionalities are ready.

Install
=======

Use nseg in your own package

    $ npm install nseg

Or if you want to use `nseg` command

    $ npm install -g nseg

Command line
============

After intsalling globally, you can use `nseg` command to:

help

    $ nseg help

segment text using default dictionary

    $ nseg segf -i ~/project/text/shi.txt -o ~/project/output/shi.txt
    $ nseg segd -i ~/project/text -o ~/project/output

build user dictionary for loading aftermath

    $ nseg dict ~/project/data/dict.js ~/dict/dict1.txt ~/dict/dict2.txt
    $ nseg dict ~/project/data/dict.js ~/dict

build character-frequecy map for loading aftermath

    $ nseg freq ~/project/data/freq.js ~/freq/data1.csv ~/freq/data2.csv
    $ nseg freq ~/project/data/freq.js ~/freq

segment text using customized settings

    $ nseg seg -d ~/project/data/dict.js -f ~/project/data/freq.js -i ~/project/text -o ~/project/output
    $ nseg seg -l ~/project/lex/ -i ~/project/text -o ~/project/output

check the existence of a word

    $ nseg check "石狮"
    $ nseg check -d ~/project/data/dict.js "石狮"

Using nseg in program
======================

Preparation
-----------

- (Optional) build your own dictionay and freqency map
- (Optional) create your own lexical handler for special text pattern

Examples
--------

````javascript
var dict  = require('../data/dict'),
    freq  = require('../data/freq'),
    date  = require('../lex/datetime'),
    sina  = require('../lex/sina');

var opts  = {
        dict: dict,
        freq: freq,
        lex: [date, sina],
    };

var nseg = require('nseg').evented(opts);

var strmOut = fs.createWriteStream(target, {flags: 'w+', encoding: 'utf-8'}),
    strmIn  = fs.createReadStream(input);

var pipe = nseg(strmIn, strmOut);
pipe.on('error', function (err) {
    console.log('error', err);
});

pipe.start();

````

Lexical handler customization
=============================

Lexical handlers support definitions by regexp patterns or acceptor functions.

License
=======

MIT License
