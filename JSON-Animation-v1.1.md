Phantom JSON Animation Standard
===============================
Version 1.0

What this standard is for
=========================
This standard is to represent an animation from a collection of frames, each as a file.

Animation Details and Composition
=================================
Each animation is simply a hash (contained in braces {}).  

Attributes
----------
 * name: The name of the animation. When converted this may be lost and is only to differentiate animations when you have multiple animations stored in the same JSON file or stream.
 * loops: The ammount of loops. 0 is the default/fallback value and is eqivilent to infinte loops.
 * skip_first: Skip the first frame when animation is supported. Depending on your implementation this may be meaningless, but in situtations where a format supports a fallback dummy frame for graceful degredation [APNG, GIF] or in situations where you run the animation as a script and that script fails to load this is useful.
 * default_delay: The default delay for frames (the delay to be used when no frame delay is specified). This can be specified as a single integer representing 1000's of a second, such as "100", or as a numerator denominator pair such as "100/1000". The default is 100/1000 (100ms).
 * frames: An array of frames, including extension. Paths can be relative/absolute/URLs, etc. Delays can be specified on each frame by specifying it as a hash within the array, using the frame file as the key and the delay as the value. Again, delays are specified as integers in 1000's of a second or as fractions of a second. Delays specified within the frames array override the delays array.
 * delays: An array of delays mapped to each frame. If there are fewer delays than there are frames the delays are looped over the animation frames, such as if you had "delays": [300, 200] and you had 3 frames, the delays would be 300, 200, 300. Delays specified in the frames array override delays specified in the delays array.

Examples
========
Simple animation
```json
{
  "name": "simple",
  "frames": ["0.png", "1.png", "3.png"]
}
```

A folder full of frames
```json
{
  "name": "more_frames",
  "frames": ["0.png", "1.png", "moreframes/*.png", "last.png"]
}
```

2 loops
```json
{
  "name": "two_loops",
  "loops": 2,
  "frames": ["0.png", "1.png", "moreframes/*.png", "last.png"]
}
```

Skip first
```json
{
  "name": "first_frame_is_fallback",
  "loops": 2,
  "skip_first": "true",
  "frames": ["0.png", "1.png", "moreframes/*.png", "last.png"]
}
```

Default delay of 2 10ths of a second (5 fps)
```json
{
  "name": "first_frame_is_fallback",
  "loops": 2,
  "skip_first": "true",
  "default_delay": "2/10",
  "frames": ["0.png", "1.png", "moreframes/*.png", "last.png"]
}
```

Delay specified for individual frames in the frames array
```json
{
  "name": "these_delays_exactly",
  "loops": 2,
  "skip_first": "true",
  "frames": [{"0.png": 200}, {"1.png": 100}, {"moreframes/*.png": 150}]
}
```

Specify a set of delays in the delays array
```json
{
  "name": "delays_delays",
  "loops": 2,
  "skip_first": "true",
  "frames": ["0.png", "1.png", "moreframes/*.png", "last.png"],
  "delays": [100, 200, "2/5"]
}
```

Specify a set of delays in the delays array with one frame delay overridden (last frame shows for a long time)
```json
{
  "name": "delays_delays",
  "loops": 2,
  "skip_first": "true",
  "frames": ["0.png", "1.png", "moreframes/*.png", {"last.png": 3000}],
  "delays": [100, 200, "2/5"]
}
```

Credits
=======
* Rei Kagetsuki, Team Phantom lead [GitHub](https://github.com/Kagetsuki) 


