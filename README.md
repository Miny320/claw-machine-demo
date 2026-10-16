# Claw Machine

A small claw machine reward game for the classroom.
It runs in the browser from one HTML file.
There is nothing to install and no login.

| Version | File | Play it here |
| --- | --- | --- |
| Halloween | `halloween/index.html` | https://claw-machine-demo.vercel.app/halloween/ |
| Original demo | `index.html` | https://claw-machine-demo.vercel.app |

<p>
  <img src="screenshots/play.png" alt="The claw lifts a toy out of the machine" width="49%">
  <img src="screenshots/win.png" alt="The win screen with the prize and confetti" width="49%">
</p>

## How to run

Open one of the links above, or run it from your own computer:

1. Download this repository.
2. Double-click `halloween/index.html`, or `index.html` for the original demo.

It opens in Chrome, Edge or Safari.
It needs no server, no build step and no internet.

## How to play

| Action | Mouse or touch | Keyboard |
| --- | --- | --- |
| Move the claw | The two arrow buttons, or tap or drag inside the glass | Left and Right arrow, or A and D |
| Drop the claw | The DROP button | Space, Enter or Down arrow |
| Play again | The Play again button | Space or Enter |
| Sound on or off | The speaker button | M |
| Full screen | The full screen button | F |

Hold an arrow button to keep the claw moving.
A quick tap moves it one small step.

In the Halloween version the claw does not carry the toy to the prize door by itself.
After the lift, the player moves it to the left with the button, the key or a tap on the glass.
When it arrives above the prize door, the claw lets the toy go.
One of the things in the machine is a mystery capsule.
It rattles in the prize tray, then cracks open on the win screen and a toy pops out, a different one each time.
Sometimes a rare golden pumpkin comes out instead, with a golden glow. It is never in the pile, and it never comes twice in a row.

The claw grabs the toy right below it.
When the claw is in the right place, that toy wiggles and the DROP button pulses.
If nothing is below the claw, it comes up empty and the player can try again.

## Features

- The claw moves, drops, closes, lifts and carries the toy to the chute.
- The motion is smooth, with a swinging cable and soft starts and stops.
- The toys sit in a pile with simple physics (six in the demo, nine plus a mystery capsule in the Halloween version), and the machine refills when it is empty.
- A win screen shows the prize with confetti, and a counter keeps the number of prizes.
- Mouse, touch and keyboard all work, also at the same time.
- The picture scales to any screen, from a phone to a 4K interactive whiteboard.
- The sounds are made in code, so there are no audio files, and the mute choice is remembered.
- It is light for old devices: fixed parts are drawn only once, and the game lowers its own resolution on a slow device.

## How it is built

- Each version is one HTML file: the page, the styles, the script and the toy pictures.
- The script is plain JavaScript on a Canvas, with no libraries.
- It uses only old (ES5) JavaScript syntax, so old tablets can run it.
- The machine, the claw, the buttons and the confetti are drawn in code.
- The only images are the toys, stored as base64 text at the bottom of the file.
- The page makes no outside requests.

## Change the game

### Settings

The `SETTINGS` block at the top of the script holds the numbers and texts that are most useful to change.

| Setting | What it does |
| --- | --- |
| `moveSpeed`, `moveAccel`, `moveBrake` | How fast the claw moves, starts and stops |
| `dropSpeed`, `liftSpeed`, `carrySpeed` | How fast the claw goes down, comes up and carries a toy |
| `grabRange` | How close the claw must be to the middle of a toy (1 is easy, lower is harder) |
| `autoAlign` | Slides the claw over the middle of the toy while it drops |
| `sound` | Sound on or off at the start |
| `title`, `startMessage`, `missMessage`, `winSign`, `winMessages`, `againLabel` | The texts on the sign, on the win screen and on the button |

### Toys in the machine

`FLOOR_ROW` and `TOP_ROW` list the toys.
Each toy has a size (`r`) and a resting tilt (`tilt`).
Each top toy rests in a gap of the floor row (`gap`).
Keep the floor row full, which means its `r` values add up to about 258.
The Halloween version has `TOP_ROWS` instead, a list of rows, and each row rests in the gaps of the row below it.

### Use another toy picture

The game treats every toy as a circle, so round toys fit best.

1. Make a PNG with a transparent background, about 640 pixels wide.
2. Turn it into base64 text (see the commands below).
3. Paste that text into the `toy-art` block at the bottom of `index.html`, in place of the old text.
   The Halloween version has one block for each toy, and the `TOY_ARTS` list says which block each toy uses.
4. Set `TOY_ART` (or the toy's line in `TOY_ARTS`) to the middle and the size of the round body of the toy.
   `cx` and `r` are fractions of the picture width, and `cy` is a fraction of its height.

Windows (PowerShell), copies the text to the clipboard:

```powershell
[Convert]::ToBase64String([IO.File]::ReadAllBytes((Resolve-Path toy.png))) | Set-Clipboard
```

Mac, copies the text to the clipboard:

```bash
base64 -i toy.png | pbcopy
```

## Tested

- Chrome and Edge on Windows, with scripted browser runs.
- Full rounds with mouse, touch and keyboard, the miss case, winning all six toys, the refill, and resizing in the middle of a round.
- Eleven screen sizes, from 320 x 480 to 3840 x 2160.
- The hosted link, with one full round in Chrome.
- No console errors and no outside requests.

Still to check by hand: Safari on an iPad or a Mac, and a real Chromebook.

## Files

| File | What it is |
| --- | --- |
| `halloween/index.html` | The Halloween version |
| `index.html` | The original demo |
| `screenshots/` | The pictures on this page |

To share a version as a zip, pack its HTML file:

```powershell
Compress-Archive -Path halloween\index.html -DestinationPath claw-machine-halloween.zip -Force
```

## Rights

This project is made for a client.
The toy illustrations belong to the client and are used here only for this game.
There is no open source licence.
Please do not copy or reuse the code or the artwork without permission.
