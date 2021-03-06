# Purpose

maxframe provides the ability to maximize the emacs frame and stay within
the display resolution.

## Usage

Example of lines to be added to your .emacs:

    (require 'maxframe)
    (add-hook 'window-setup-hook 'maximize-frame t)

If using two framebuffers (monitors), it might be necesssary to specify a
mf-max-width value set to the pixel width of main framebuffer.  This is
necessary because emacs does not yet support sniffing different
framebuffers.  Example:

    (require 'maxframe)
    (setq mf-max-width 1600)  ;; Pixel width of main monitor.
    (add-hook 'window-setup-hook 'maximize-frame t)

To restore the frame to it's original dimensions, call restore-frame:

    M-x restore-frame

## How it works

puts the emacs frame in the top left corner of the display and calculates
the maximum number of columns and rows that can fit in the display

## Alternatives

There is a good list of [full-screening alternatives on the Emacs Wiki](http://emacswiki.org/emacs/FullScreen).

### On a Mac?

While I still have maxframe in my emacs initialization, I only use it as a
backup for when `ns-toggle-fullscreen` is not present. I compile emacs with
native fullscreen support now, and it's pretty nice. If you use
[homebrew](https://github.com/mxcl/homebrew), here's the compilation step
that'll do it for you.

```bash
$ brew install emacs --srgb --cocoa
```

See the relevant portion of
[my emacs config](https://github.com/rmm5t/dotfiles/blob/master/emacs.d/rmm5t/maxframe.el)
to see how to make the distinction between `ns-toggle-fullscreen` and
`maxframe`.

## Limitations

Requires Emacs 22 (for fringe support), but maximize-frame still works
under Emacs 21 on Windows.

Emacs does not recognize when the display's resolution is changed. This is
a problem because I would like to be able to re-maximize the frame after
connecting to a display with different resolution. Unfortunately,
display-pixel-width and display-pixel-height yield the display resolution
values from when emacs was started instead of the current display
values. Perhaps there's a way to have emacs re-sniff these values, but I'm
not yet sure how.

## Credits

The w32 specific functions were borrowed from the Emacs Manual:
http://www.gnu.org/software/emacs/windows/big.html#windows-like-window-ops
