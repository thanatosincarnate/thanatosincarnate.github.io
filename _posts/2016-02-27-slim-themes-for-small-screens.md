---
layout: post
title: Slim Themes for Small Screens
---

On recent posts, I have lamented how new GUI development in Linux is rather geared towards full HD screens, i.e. 1920x1080 resolution, or even 4K displays. If you're like me, however, you won't give up on your hardware with a lower screen resolution just because certain developers won't consider them. In fact, if you stick to mostly GTK2 or QT programmes and don't depend too much on GTK3, chances are lower resolutions can be used well for production systems. Here are my tips, some more obvious than others, on how to increase screen real estate:

## The more obvious ones

I'll be working with traditional desktop metaphors, as UIs such as Gnome, Unity etc. require a more hands on approach with theming. My machine has an 1366x768 resolution and runs Xfce, so for a slimmer look, I trim the following settings:

<table>
  <tbody>
    <tr>
      <td>Panel height ("Row size" on Xfce)</td>
      <td>18</td>
    </tr>
    <tr>
      <td>Font and size</td>
      <td>Droid Sans 8; Ubuntu Mono 10 for consoles</td>
    </tr>
    <tr>
      <td>DPI</td>
      <td>96</td>
    </tr>
  </tbody>
</table>

## Themes

It's easy to find some older GTK2 themes that have been slimmed down. The most popular used to be <a href="http://martin.ankerl.com/2007/11/04/clearlooks-compact-gnome-theme/">Clearlooks Compact</a>. If you look over the creator's site, there is a screenshot which you can mouse over and see the difference. The compact version of the theme takes up much less of your screen. However, while this theme gives good visibility and sports some pleasant colours, chances are the old-fashioned look won't make you really happy. You can though open up the gtkrc file of Clearlooks Compact and compare it to your favourite GTK2 theme. Adjusting the different **size** values, as well as **xthickness** or **ythickness** can save a lot of visual padding that very often is not needed for clarity and only takes away needed space:

{% highlight js %}
        xthickness = 1
        ythickness = 1
{% endhighlight %}

Another set of offenders are at the top of the file - the icon sizes:

{% highlight js %}
gtk-icon-sizes = "panel-menu=16,16 : gtk-menu=16,16 : gtk-button=16,16 : gtk-small-toolbar=16,16 : gtk-large-toolbar=16,16 : gtk-dialog=32,32 : gtk-dnd=32,32"
{% endhighlight %}

Here, they've almost all been changed down to 16x16, which is more than enough on lower resolutions.

You can experiment with these values and compare it to the original theme by switching between them. I'm currently doing this with the lovely Arc theme, the results of which you can see below. I've also reduced the size of my Xfwm theme, but more on that in the follow up.

![placeholder](https://i.imgur.com/gdfaVlE.jpg "Arc theme comparison - original and slim")


I'll of course post the code of my slimmer theme once I'm done.

