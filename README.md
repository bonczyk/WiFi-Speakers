# WiFi-Speakers
Play Windows audio on Linux PC (DD-WRT) with USB speakers via esounD deamon

<li><code>linein180.exe</code> - virtual sound line that captures all Windows audio </li>
<li><code>out_esd.dll</code> - Winamp 2 plugin that play from virtual sound device to esounD</li>
<li><code>esd</code> - linux esounD deamon</li>

<h1>Using the WL-500g as a wireless soundcard</h1>
With an external USB soundcard and <a href="http://wl500g.dyndns.org/">Oleg's
modified firmware</a>, an ASUS <a
 href="http://www.asus.com/products4.aspx?l1=12&amp;l2=43&amp;l3=0&amp;model=61&amp;modelmenu=1">WL-500g</a>
WLAN router can be used to
wirelessly play music on your stereo using Winamp or almost any Linux
sound player.<br>
<h2>Installing EsounD on the WL-500g</h2>
<p>For receiving sound streams on the router and playing them on the
USB
sound card, the well-kown <a
 href="http://www.tux.org/%7Ericdude/EsounD.html">EsounD</a> daemon is
used. You can either install it as an ipgk from Unslug or download the
binary file from this location: <br>
</p>
<div style="margin-left: 40px;">EsounD daemon binary: <a
 href="http://home.in.tum.de/%7Epustka/mipsel/esd">esd</a> <br>
</div>
<p>Before starting it, the default ASUS sound server (useable only from
Windows Media Player) needs to be killed, as it occupies the sound
card:
</p>
<div style="margin-left: 40px;"><code>killall waveservermain</code><br>
<code>killall waveserver</code><br>
</div>
<p>Then the ESD daemon can be started:<span
 style="font-family: monospace;"></span></p>
<div style="margin-left: 40px;"><span style="font-family: monospace;"></span><code>esd-d /dev/sound/dsp -tcp -public &amp;</code><br>
</div>
<h2>Connecting to the soundcard from a client computer</h2>
<p>If you are running Linux, you can use an audio player like <a
 href="http://www.xmms.org/">XMMS</a> or <a
 href="http://amarok.kde.org/">amaroK</a>, choose an EsounD output
plugin (gstreamer in case of amaroK) and enter the server's IP address.
</p>
<p>In order to connect to the EsoundD server from Windows, Kasper
Laudrup
has a nice EsounD output plugin for <a href="http://www.winamp.com/">Winamp</a>
available at&nbsp; <a href="http://www.linuxfan.dk/index.php?page=code">his
site</a>. Note that for Winamp 5 you need to download the Winamp 2
version, not Winamp 3. At the bottom of this page, there also is a link
to an updated version, which includes better resampling.<br>
</p>

