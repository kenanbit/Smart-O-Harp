## Summary

This site details an ongoing project to improve the chord selection mechanism on chromatic Autoharps/Chromaharps (hereafter called just "autoharps"). An arduino reads inputs from a keypad, computes the desired chord from the keypresses, and mechanically dampens the undesired strings. 

It does *not* strum or pluck for the human, nor does it change chords without human input.

See [Motivations](#motivation) for why this project is useful.

See [Dampening Mechanism](#dampening-mechanism) for an for detailed analysis of dampening mechanism possibilities.

--------

## Motivation
#### Autoharps are limited in number/variety of chords

Most autoharps have between 12 and 21 chord bars, with the ability to play in only some of the 12 musical keys. The chords available are usually major chords, minor chords, major-minor 7 chords, and sometimes a diminished chord.

Thinking just about these 4 types of chords, the maximal manual autoharp can play 21 of them, out of the `12*4=48` possible.

Stepping out of the chord bar paradigm can allow more flexibility.

#### Ergonomics of chord layouts can only go so far, and are not always key agnostic

The best layout I've found with 21 bars is to have each column be of the form (from farthest reach with the left hard to closest): `(Am, C, A7)`. Successive columns just walk this around the circle of fifths. This makes playing most major and minor songs in 5 key signatures ergonomic and *key agnostic* (transposing a song is as simple as shifting your chording hand over). Still, one of several flaws with this layout: When one wants the major/minor version of the minor/major chord, it's a wide reach that may go off the harp.

Stepping out of the 1 button = 1 chord paradigm can allow more flexibility.

#### Playing autoharps for long periods can cause cramping, arthritis, or other joint pain in the chording hand.

Depending on how well tuned the harp is and how the hand is positioned, this may be more or less of an issue. I don't play for more than an hour at a time, due to cramping.

Stepping out of the finger-force dampening paradigm etc.

----------

## Dampening mechanism

3 possibilities for this:

#### One solenoid per string

This is my current favorite. Every string has a small solenoid positioned so that the unpowered state is dampening the string. When powered, the dampener lifts up, allowing that string to sound. The arduino controls the 30-40 solenoids individually, allowing more flexibility than the other two solutions. Cheap solenoids will cost around $1.

**Construction summary**: From a autoharp with exposed chord bars. Remove all bars except for one. Stretch the springs holding that bar so that the bar stays high under more force. Super glue solenoids to the sides of the bar such that the solenoids head is just short of touching the string it should dampen. Padding can then be glued to the head of the solenoid so that the resting state dampens the string effectively. Alternate placing solenoids on each side of the bar to give them enough lateral space.

**Considerations**: Size, shape, material of the dampening pads. Force of dampening. Lower notes' pads need more contact with the string to effectively dampen.

**Pros**: String by string flexibility for chord building, simple construction

**Cons**: Raised solenoids (undampened strings) draw current while remaining raised. (TODO power/battery requirements.)

#### Depress single-note bars with motor push

This is the second simplest solution. There are 12 "chord" bars, but their felts are cut so that one dampens only the `C`s, one dampens only the `C#`s, etc. Now to form an arbitrary chord, press down the set of bars that correspond to the pitch classes you **don't** want in the chord. Each depression will require more force than solenoids can probably supply, so higher torque stepper motors may be better.

**Construction summary**: From an autoharp with exposed chord bars, take 12 bars and cut their felts to only dampen one pitch class. Replace them in a way to avoid damping on harmonic nodes. Get 12 high torque stepper motors with arms that swivel to straight down (to depress a bar). Mount them above the bars somehow, taking into account their difficult dimensions and the point of downward force on the bar relative to the strings being dampened. Given my lack of construction experience, this last task was too daunting for me.

**Considerations**: Force of dampening. Avoiding harmonic nodes.

**Pros**: Minimal power usage when not changing chords. Probably cheaper than the solenoids if done right, but not by much.

**Cons**: Complicated mounting that occupies space in front of chord bars, which may get in the way of the strumming hand.

#### Depress single-note bars with down pulling strings

Like the last in terms of the single note bars. For each bar: Tie a string to each end, run it straight downward and around a pivot point, then pull on both ends to depress the bar. Use a motor head to pull the strings taut to dampen a note.

**Considerations**: Allowing the motors to do no work when not changing chords. Motors need to be about as high torque as previous.

**Pros**: The complicated mounting of the previous can be relocated somewhere less invasive (inside the autoharp body would be really interesting.

**Cons**: Starting to get quite complicated.

#### Avoiding harmonic nodes (TODO)

#### Keypad &rarr; Notes logic (TODO)

#### Arduino setup (TODO)
