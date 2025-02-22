# Lucy's dwm

# Patches

Patches and their explanation and what they do


## actualfullscreen
Actually toggle fullscreen for a window, instead of toggling the status bar and the monocle layout.

## # attachaside
Make new clients get attached and focused in the stacking area instead of
always becoming the new master. It's basically an attachabove modification.
```Original behaviour :
+-----------------+-------+
|                 |       |
|                 |   P   |
|                 |       |
|        N        +-------+
|                 |       |
|                 |       |
|                 |       |
+-----------------+-------+
New Behaviour :
+-----------------+-------+
|                 |       |
|                 |   N   |
|                 |       |
|        P        +-------+
|                 |       |
|                 |       |
|                 |       |
+-----------------+-------+
+-----------------+-------+
|                 |       |
|                 |   P   |
|                 |       |
|                 +-------+
|                 |       |
|                 |   N   |
|                 |       |
+-----------------+-------+
```


## autoresize
By default, windows that are not visible when requesting a resize/move won't
get resized/moved. With this patch, they will.

## autostart
This patch will make dwm run &quot;~/.dwm/autostart_blocking.sh&quot; and
&quot;~/.dwm/autostart.sh &amp;&quot; before entering the handler loop. One or both of these
files can be ommited.
Be aware that dwm will not startup as long as autostart_blocking.sh is running
and will stay completely unresponsive. For obvious reasons it is generally a
bad idea to start X-applications here :)

## barpadding
This patch adds variables for verticle and horizontal space between the statusbar and the edge of the screen; unlike statuspadding, which adds padding between the bar's content and the edge of the bar. This patch adds two new variables (both default to 10) to config.def.h:

- `vertpad` (amount of vertical padding)
- `sidepad` (amount of padding either side of the bar)

## colorbar
This patch lets you change the foreground and 
background color of every statusbar element.
Simply change the RGB values in the config.def.h.

## fancybar
This patch provides a status bar that shows the titles of all visible windows
(as opposed to showing just the selected one). When the titles don't completely
fit, they're cropped. The title of the selected window is inverted.

## stacker
This patch provides comprehensive utilities for managing the client stack. It
implements two new commands: `focusstack` (which is a replacement for the
original `focusstack` command) and `pushstack`. The first one is for focusing
clients while the second one moves clients around the stack. Both commands take
the same kind of argument:

- Pass `PREVSEL` to focus/push the previously selected client in the current
tagset.
- Pass `INC(+/-inc)` to focus/push relatively to the selected client. This will
wrap around the stack limits.
- Pass a positive number to focus/push relatively to the beginning of the
stack. Out of limit values will be truncated to the position of the last
visible client and won't wrap
around.
- Pass a negative number to focus/push relatively to the last visible client in
the stack. Here -1 means the last client, -2 the previous to last client, etc.
Out of limit values will be truncated to the position of the first visible
client (0) and won't wrap around.

## Default key bindings
There are two parallel sets of bindings: one for the `focus*` family and the
other for the `push*` family. The keys are the same for both sets but they do
differ in the modifiers: simply `MODKEY` for the `focus*` family and
`MODKEY|ShiftMask` for the `push*` family.
``` Key   Argument   Description
---------------------------------------
 \     PREVSEL    Previously selected
 j     INC(+1)    Next to selected
 k     INC(-1)    Previous to selected
 q       0        First position
 a       1        Second position
 z       2        Third position
 x      -1        Last position
```
The `q`, `a`, `z` keys are aligned more or less vertically in the us keyboard
layout. They are intended to be used as quick positional shortcuts to specific
applications. So if you have 9 tags you get 9*3=27 shortcuts in a two-level
hierarchy of clients. The ` key is above the `Tab` key and it's intended to
complement the &quot;move to previously selected tag&quot; function of dwm at the
intra-tag level. Finally, the `x` key is like &quot;I don't care so much about you
just right now but you can still live in this tag&quot;.
Notice that `MODKEY|ShiftMask+q` collides with the default binding for quitting
dwm, which stacker changes to `MODKEY|ShiftMask+BackSpace`.

## systray
A simple system tray implementation. Multi-monitor is also supported. The tray
follows the selected monitor.
In case icons disappear when toggling the bar, try a different font size
in dwm. This has helped at least in one case with pidgin.


