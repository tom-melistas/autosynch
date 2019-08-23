# autosynch

[![Build Status](https://travis-ci.com/SwagLyrics/autosynch.svg?branch=master)](https://travis-ci.com/SwagLyrics/autosynch) [![codecov](https://codecov.io/gh/chriswang030/autosynch/branch/phase2/graph/badge.svg)](https://codecov.io/gh/chriswang030/autosynch)

## about
Given an audio file of some recognizable song, autosynch will try to align its
lyrics to their temporal location in the song. The song lyrics must be available
on <genius.com>.

## installation
To install, do the following:
- `git clone`
- `cd autosynch`
- `pip install -r requirements.txt`

## dependencies
Using autosynch requires a trained model for vocal isolation as well as
PortAudio. For mp3 support, SoX is required. On MacOS/Linux, get everything by
executing:
- `./setup.sh`

If permission is denied, first execute:
- `chmod a+rx setup.sh`

### download model
If you would like to download the weights manually or get a different version,
check here:
- [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3334973.svg)](https://doi.org/10.5281/zenodo.3334973) for weights trained on MedleyDB V1
- [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3351632.svg)](https://doi.org/10.5281/zenodo.3351632) for weights trained on MedleyDB V2

Weights must be placed into `autosynch/mad_twinnet/outputs/states`.

### install portaudio
On Mac:
- `brew install portaudio`

On Linux:
- `sudo apt-get update`
- `sudo apt-get install portaudio19-dev`

### install sox
Note: Installing SoX is optional and only required for processing mp3 files.

On Mac:
- `brew install ffmpeg`

On Linux:
- `sudo apt install ffmpeg`

## usage
To play a song with its lyrics displayed at its calculated position:
- `python3 autosynch/playback.py <audio_file.wav> <artist_name> <song_title>`
It will take a few minutes to perform the alignment process.

Alternatively, if you have already generated an alignment file using
`autosynch.align.line_align`, you may also execute:
- `python3 autosynch/playback.py <audio_file.wav> <align_file.yml>`

If you would like to process an mp3 file instead, see [this section](#install-sox).

Note: If you did not use `setup.sh`, first make sure you set your Python
environment correctly with `export PYTHONPATH=$PYTHONPATH:./` from the outer
`autosynch` directory.
