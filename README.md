PHP Reader (Zend Mp3)
=====================

The PHP Reader is a library written in PHP to read and write media files and their information headers in an object-oriented manner. Currently supported formats are ASF (Windows Media Player files, i.e. WMA, WMV, etc), ID3, including both ID3v1 and ID3v2 (MPEG files, i.e. MP3), MPEG Audio Bit Stream (i.e. ABS, MP1, MP2, MP3), MPEG Program Stream (MPEG movies, and DVD and HD DVD video discs, i.e. MPG, MPEG, VOB, EVO), and ISO Base Media File Format (eg QuickTime, MPEG-4 and iTunes AAC files, i.e. QT, MOV, MP4, M4A, M4B, M4P, M4V, etc).

The library was written by Sven Vollbehr and is hosted originally at [Google Code](https://code.google.com/p/php-reader/). This Github fork just adds support for the PSR-0 autoloading standard for Composer.

## Installation

Install PHP Reader with [composer](https://getcomposer.org) via

    composer require debach/zend-mp3:dev-master
    composer install

## How to use PHP Reader

PHP reader has a [nice documentation](https://code.google.com/p/php-reader/) both on its website and in the code. What follows are a couple of examples to give you a quick start. PHP reader can do a lot more that what is covered here.

### Reading the duration of an MP3 file

To retrieve the *estimated* duration in seconds from an MP3 file, proceed as follows:

    $abs    = new Zend_Media_Mpeg_Abs('file.mp3');
    $length = $abs->getLengthEstimate();

You can get the *exact* duration with `$abs->getLength()`, but it requires to read *every frame* of the MP3 file. Usually, the estimated duration is already very accurate and much faster.

### Reading ID3 tags

Use the `Zend_Media_Id3v2` class to read or write ID3 information ([official documentation](https://code.google.com/p/php-reader/wiki/ID3v2)):

    $id3   = new Zend_Media_Id3v2('file.mp3');
    
    $frame = $id3->getFramesByIdentifier('TIT2'); // for song title; or TALB for album title; ..
    $title = $frame[0]->getText();
    
    $frame = $id3->getFramesByIdentifier('TALB');
    $album = $frame[0]->getText();
