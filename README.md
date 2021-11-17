# Music-Triangle

### “Without music, life would be a mistake” ---Friedrich Nietzsche

***

## Super-efficient and capable MIDI music AI encoding/tokenization strategy proposal

***

### Basic Concepts

1) Break down standard MIDI composition into pitches/time-shifts sequences

2) We only use pitches values and delta start-times to encode all music info

3) Once the model is created and output sequence is generated, music info is restored back by using a fuzzy music triangle ratio calculations

***

### Music Triangle Diagram

<img width="512" src="https://github.com/asigalov61/Music-Triangle/raw/main/Music%20Triangle-Diagram.png">

#### LEGEND

1) [delta start-time] dt == delta start-time (0-127)
2) [MIDI pitch[ P == MIDI pitch (0-127)
3) [duration[ D == sqrt(dt^2 + P^2) (0-127)
4) [velocity[ V == P (0-127) or you can do whatever here (i.e inversion or cosine...)

***

### Proposed Encoding/Tokenization Sequence Info

1) Variable sequence length
2) Pitch/time-shift data is encoded as (0-127) for notes/chords pitches and (128-255) for time-shift/EOS tokens
3) I.e. [21, 64, 60, 57, 215, 33, 64, 60, 55, 215, 36, 72, 183, 64, 161]

### Citation

```bibtex
@inproceedings{lev2021musictriangle,
    title       = {Music Triangle},
    author      = {Aleksandr Lev},
    booktitle   = {GitHub},
    year        = {2021},
}
```

***

### Project Los Angeles

### Tegridy Code 2021


