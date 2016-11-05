---
layout: post
title: A Look Beyond to Debian 9 Stretch
---

Now that the various freezes are almost upon us Debian users, I thought it would be useful to look at what will change with the new release. Obviously, with the long wait time between two consecutive Debian releases, a lot will move forward and a lot of it is by no means news. With our very conservative update strategy, we Debian users have a big portion of catching up to do, but I find that using Stable in an environment where stability is key and big strides in features are not essential makes the wait worthwhile -- for one, we get all the new goodies of free software as a big present, and as an added bonus, our careful update strategy gives us a polished product with a lot of the teething troubles and other nasty bugs ironed out. This look ahead is geared towards what I consider to be typical desktop use cases and should by no means be considered an exhaustive list.

## The Story Thus Far

As a reminder, let's take a look at where we are now and where the journey will take us:

Debian Stable

<table>
  <tbody>
    <tr>
      <td>Debian GNU/Linux 8 Jessie</td>
      <td>Released: April 26th 2015</td>
      <td>Tentative Stretch Release: Mid 2017?</td>
    </tr>
    <tr>
      <td>Kernel</td>
      <td>3.16 (Backports: 4.7)</td>
      <td>4.10</td>
    </tr>
    <tr>
      <td>Xorg Server</td>
      <td>1.16.4</td>
      <td>1.18.4</td>
    </tr>
    <tr>
      <td>Xorg</td>
      <td>7.7</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>Mesa</td>
      <td>10.3.2 (Backports: 12.0.3)</td>
      <td>12.x</td>
    </tr>
    <tr>
      <td>HPLIP</td>
      <td>3.14.6 (Backports: 3.16.9)</td>
      <td>>=3.16.x</td>
    </tr>
    <tr>
      <td>Gnome</td>
      <td>3.14</td>
      <td>3.22</td>
    </tr>
    <tr>
      <td>KDE</td>
      <td>4.14.2</td>
      <td>5.8</td>
    </tr>
    <tr>
      <td>Xfce</td>
      <td>4.10.1</td>
      <td>4.12.1</td>
    </tr>
    <tr>
      <td>Mate</td>
      <td>1.8.1</td>
      <td>1.16.1</td>
    </tr>
    <tr>
      <td>Cinnamon</td>
      <td>2.2.16 (Backports: 3.0.4)</td>
      <td>3.0.7</td>
    </tr>
    <tr>
      <td>Shotwell</td>
      <td>0.20</td>
      <td>0.24</td>
    </tr>
    <tr>
      <td>Digikam</td>
      <td>4.4 (Backports: 4.14)</td>
      <td>5.2</td>
    </tr>
    <tr>
      <td>LibreOffice</td>
      <td>4.3.3 (Backports: 5.2.3)</td>
      <td>5.2.3</td>
    </tr>
    <tr>
      <td>Gimp</td>
      <td>2.8.14</td>
      <td>2.8.18</td>
    </tr>
    <tr>
      <td>Darktable</td>
      <td>1.4.2 (Backports: 2.0.4)</td>
      <td>2.0.7</td>
    </tr>
    <tr>
      <td>Inkscape</td>
      <td>0.48.5 (Bacports: 0.91)</td>
      <td>0.91</td>
    </tr>
    <tr>
      <td>Scribus</td>
      <td>1.4.4</td>
      <td>1.4.6</td>
    </tr>
    <tr>
      <td>LaTeX (TeX Live)</td>
      <td>20141024</td>
      <td>20161008</td>
    </tr>
    <tr>
      <td>Kdenlive</td>
      <td>0.9.10</td>
      <td>16.08</td>
    </tr>
    <tr>
      <td>Openshot</td>
      <td>1.4.3</td>
      <td>1.4.3</td>
    </tr>
    <tr>
      <td>Pitivi</td>
      <td>0.93</td>
      <td>0.97</td>
    </tr>
  </tbody>
</table>

