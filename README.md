# Music Triangle

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

1) [delta start-time] dt == t - pt | range(0-127)
2) [MIDI pitch] P == P | range(0-127)
3) [duration] D == sqrt(dt^2 + P^2) | range(0-127)
4) [velocity] V == P | range(0-127) or you can do whatever here (i.e inversion or cosine...)

***

### Proposed Encoding/Tokenization Sequence Info

1) Variable sequence length
2) Pitch/time-shift data is encoded as (0-127) for notes/chords pitches and (128-255) for time-shift/EOS tokens
3) I.e. [21, 64, 60, 57, 215, 33, 64, 60, 55, 215, 36, 72, 183, 64, 161]

***

### Model output decoding example

```
if len(out) != 0:
  song = []
  sng = []
  for o in tqdm.tqdm(out):
    
    if o < 128:
      sng.append(o)
    else:
      if len(sng) > 0:
        sng.append(o-127)
        song.append(sng)
        sng = []


  song_f = []
  time = 0
  for s in tqdm.tqdm(song):
    for ss in s[:-1]:
        
        song_f.append(['note', time, s[-1] * 15, 0, ss, ss])
    time += (s[-1] * 5)

  detailed_stats = TMIDIX.Tegridy_SONG_to_MIDI_Converter(song_f,
                                                        output_signature = 'Project Los Angeles',  
                                                        output_file_name = 'Music-Triangle-Composition', 
                                                        track_name='Tegridy Code 2021', 
                                                        number_of_ticks_per_quarter=500)
  print('Done!')
    
detailed_stats

```

***

### Dataset/detokenization ratios/restore coefficient calculation

1) Multiplication coefficients are dataset dependent
2) Coefficients from a large dataset can be transposed to a smaller subset with good results
3) Coefficients, in this case, are dt and D averages for the entire dataset
4) For example, coefficients(k) for the provided sample INTs dataset are dtk == 12, Dk == 72
5) Or namely dtk == 1, Dk == 6
6) Since sample INTs dataset timings were dividied by 5, final coefficients are: dtk == 5, Dk == 30, which will produce nice sustained durations

***

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


