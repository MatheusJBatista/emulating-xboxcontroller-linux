
# emulating-xboxcontroller-linux
Emulating generic joypad as xbox


# Test Joypad
Download:
sudo apt-get install joystick
sudo apt-get install jstest-gtk

[Image]

## Xboxdrv
sudo apt-get install xboxdrv

## Configuring xboxdrv
On your terminal type: evtest

[Image]
Then select your joypad.

[image]
After you select the joypad, when you press any button of you joypad, they will trigger and send you a message with buttonId

[Image]

Now you have to map your buttonId with xboxdrv buttonId, like this:
where joypadButtonId=xboxdrvButtonId

--evdev-absmap<br>
ABS_X=x1<br>
ABS_Y=y1<br>
ABS_RZ=y2<br>
ABS_Z=x2<br>
ABS_HAT0X=dpad_x<br>
ABS_HAT0Y=dpad_y<br>

--evdev-keymap<br>
BTN_C=a<br>
BTN_NORTH=x<br>
BTN_SOUTH=y<br>
BTN_EAST=b<br>
BTN_Z=rb<br>
BTN_TR=rt<br>
BTN_WEST=lb<br>
BTN_TL=lt<br>
BTN_TR2=start<br>
BTN_TL2=back<br>
BTN_SELECT=tl<br>
BTN_START=tr<br>

see this image as reference:<br>
![https://steamcommunity.com/app/236090/discussions/0/558748653724279774/](https://lh4.googleusercontent.com/-IYeHo2Xb820/UwaPEr2W-7I/AAAAAAAAGpw/ysXgr-l2o_Q/w462-h383-no/xbox.jpg)

and create script replacing your map like this:<br>
xboxdrv \
--evdev /dev/input/event1 \
--evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RZ=y2,ABS_Z=x2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
--axismap -Y1=Y1,-Y2=Y2 \
--evdev-keymap BTN_C=a,BTN_NORTH=x,BTN_SOUTH=y,BTN_EAST=b,BTN_Z=rb,BTN_TR=rt,BTN_WEST=lb,BTN_TL=lt,BTN_TR2=start,BTN_TL2=back,BTN_SELECT=tl,BTN_START=tr \
--mimic-xpad --silent &

now when you type "evtest" on your terminal, there is a new device
[Image]

## Testing
*the xbox controller can take some seconds to start working*.

You can test through "evtest" selecting the xbox device and pressing any button.
[Image]

or via jstest selecting the new device on there.
[Image]

## Reference
https://steamcommunity.com/app/236090/discussions/0/558748653724279774/
