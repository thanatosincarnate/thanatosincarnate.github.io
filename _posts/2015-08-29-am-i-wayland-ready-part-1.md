---
layout: post
title: Am I Wayland Ready? - Part 1 
---


![placeholder](https://i.imgur.com/wcK41Ch.png "LibreOffice Gnome Mockup")

I'm writing this from Fedora 22 Workstation within Wayland. Yes, a quite stable Wayland at that. I'm actually very positively surprised at how well it works. There are however many things to iron out until we can truly say it works out of the box. From my short venture into Wayland Land, I don't think that the software already supporting it is giving us the most headache now. It's rather the Xorg stuff running via XWayland that is buggy at the moment. I deliberately took a more stable distro with more matured Wayland/Xorg code to avoid the initial regressions and other grave bugs distros like Arch or other experimental Wayland live CDs might have.

The laptop I used for testing:

<table>
  <tbody>
    <tr>
      <td>Acer Aspire E15 E5-521-G</td>
    </tr>
    <tr>
      <td>AMD A8-6410 APU 4 cores</td>
    </tr>
    <tr>
      <td>4 GB, 768 MB reserved for integrated AMD Radeon R5 GPU</td>
    </tr>
    <tr>
      <td>Dedicated AMD Radeon R5 M240 with 2 GB VRAM</td>
    </tr>
  </tbody>
</table>

I will not tackle this question from a developer's standpoint. This is rather an outlook of what casual desktop users might expect when taking the plunge right now. Be aware though that few stable distros offer a decent Wayland experience at the moment. Most of those are probably limited to Gnome 3.14+ (although I think 3.16 should be the bare minimun), KDE 5.x and maybe E19. So, if you're using Xfce or barebone window manager configs, your situation might be a bit more dire. The question in this article is: Would I be ready for an early adoption of Wayland? I will first present my initial experience and then give a table with vital programmes I need on a desktop with their current state on Wayland.

Finally I could see all the benefits of Wayland first hand, or so I thought. :) My main gripe with X was always how hacky it was when it comes to proper vsync support, compositing or displaying stuff like a video within a browser window, while simultaneously trying to keep both the video and the window in sync when e.g. the user scrolls down to see some text (which happens often when watching a Youtube video and reading comments). All of GTK3 more or less runs under Wayland (although in some cases programmes might activate X specific things that are then probably translated to Xwayland). Those run quite well, but those are sadly the desktop level applications I least work with on a serious desktop. Gnome may be a slick desktop, but it lacks the serious applications we find in desktop agnostic software.

Starting programmes that still run under X looked a bit weird -- a window would start which quickly flashes black and then the window content appeared. It seemed a bit like the small glitches you see when running a Wine programme. The theme and font hinting look the same as the Wayland native applications though, so it never looks out of place. LibreOffice was the only exception, as it had a smaller UI font than what was set up on the system:

![placeholder](http://i.imgur.com/zfqKJkM.jpg "Libreoffice under Wayland")

I've worked a bit with Inkscape and Gimp and both worked great, although my tests only included opening large files and looking at the output of top when scrolling within them or selecting individual items from the document. One very annoying thing which was fixed in recent verions of whatever software is responsible for it is the fact that you cannot copy/paste text from a Wayland native application to an Xorg one and vice versa.

Speaking of top, applications running under Xwayland do tax the CPU more than when they run in native X. On my low-end 4 core AMD APU with barely 2 GHz this was somewhere around 60% when the programme in question was not idling. Things, while certainly not crashing left and right, will feel wonky with the occasional performance hick up. The worst offender was Firefox. Granted, I tested Facebook and Youtube, which are performance hogs on Firefox even on X and aren't as smooth as on e.g. a browser with decent multithreading and 3D acceleration like Chrome (cough, cough). Firefox is working on its GTK3 port and multithreading, so that just might be a question of time. This is the only way I could test any video performance. Videos in Youtube were a bit more laggy than in X and certainly took more CPU power. The vsync issues were the same as in X, which is expected. Firefox is not Wayland native, so it gets no perks from it either -- vsync was not an issue in fullscreen, but outside of it, it was. I could not test any normal videos that run native in Wayland, since Totem would just segfault on me all the time.

What I could do quickly was to install Epiphany (which I think runs Wayland native as a GTK3 programme) and try out Youtube. The site would either load and display correctly or it would be blank:

![placeholder](http://i.imgur.com/MvsY1Cw.jpg "Epiphany fails to show Youtube videos")

In either case, I could still click links (even when the site appeared blank, I could click blindly) and start videos I'd hear but wouldn't see. At least with my ATI setup, it seems that the video layers aren't properly used with this version of Wayland.

Regarding video games, I ran a quick test with Guacamelee, which ran just as fine and snappy as in X. This isn't a demanding game however. Querying glxinfo, I could even see that the DRI_PRIME flag correctly recognised my discrete ATI video card. This probably means that most Xorg features will just work in Xwayland. Running a Wine game was a different matter altogether. I fired up Playonlinux, which I used to install "Vampire, the Masquerade -- Redemption". I know, it's an ancient game, but it runs 3D acceleration, so it's good enough for a test. It crashed on me:

![placeholder](http://i.imgur.com/roryGyr.jpg "Wine game won't start under Wayland")

and Playonlinux's debug window had this to say about it:

{% highlight js %}
err:x11settings:X11DRV_ChangeDisplaySettingsEx No matching mode found 1366x768x32 @0! (XRandR)
fixme:d3d:resource_check_usage Unhandled usage flags 0x8.
wine: Unhandled stack overflow at address 0x7bc64f94 (thread 0009), starting debugger...
err:seh:setup_exception_record stack overflow 880 bytes in thread 0009 eip 7bc592f1 esp 00240fc0 stack 0x240000-0x241000-0x340000
{% endhighlight %}

Hopefully this was an informative insight into what to expect on a system with Wayland. Be warned though that the software stuck I'm currently running is already outdated when it comes to the currently very speedy Wayland development. To see what the stuff is really like, I recommend taking the time and running maybe a more recent setup on Arch with a more recent kernel, Wayland, Xorg and 3D drivers (also note that Wayland currently only runs with video drivers that can do kernel modesetting). I plan on doing another follow up with the current state of video drivers, 3D gaming and video playback.

Here is a list of programmes I find essential and their current state in Wayland:

<table>
  <thead>
    <tr>
      <th>Tools:</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Archiving</td>
      <td>file-roller</td>
      <td>DONE</td>
    </tr>
    <tr>
      <td>File Search</td>
      <td>Gnome, KDE, Catfish</td>
      <td>DONE</td>
    </tr>
    <tr>
      <td>Editor</td>
      <td>vim, gedit</td>
      <td>DONE</td>
    </tr>
    <tr>
      <td>Calculator</td>
      <td>galculator</td>
      <td>DONE</td>
    </tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th>Media:</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Music</td>
      <td>Gnome, KDE, Audacious </td>
      <td>DONE</td>
    </tr>
    <tr>
      <td>Video</td>
      <td>Totem, mpv, VLC</td>
      <td>WIP</td>
    </tr>
    <tr>
      <td> </td>
      <td>Kdenlive</td>
      <td>DONE</td>
    </tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th>Productivity:</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Office</td>
      <td>Libreoffice</td>
      <td>WIP</td>
    </tr>
    <tr>
      <td>Annotation</td>
      <td>Xournal</td>
      <td>WIP</td>
    </tr>
    <tr>
      <td>Graphics</td>
      <td>Gnome</td>
      <td>WIP</td>
    </tr>
    <tr>
      <td>Vector</td>
      <td>Inkscape</td>
      <td>WIP</td>
    </tr>
    <tr>
      <td>DTP</td>
      <td>Scribus</td>
      <td>DONE</td>
    </tr>
    <tr>
      <td>Colour picker</td>
      <td>gcolor3</td>
      <td>DONE</td>
    </tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th>Games:</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Native</td>
      <td>XWayland </td>
      <td>WIP</td>
    </tr>
    <tr>
      <td>Windows</td>
      <td>Wine</td>
      <td>:(</td>
    </tr>
  </tbody>
</table>

