:notoc:

***********************
MoviePy documentation
***********************

.. image:: /_static/medias/logo.png
    :width: 50%
    :align: center

**Date**: |today| **Version**: |version|

**Useful links**:
`Binary Installers <https://pypi.org/project/moviepy/>`__ |
`Source Repository <https://github.com/Zulko/moviepy>`__ |
`Issues & Ideas <https://github.com/Zulko/moviepy>`__ |
`Q&A Support <https://www.reddit.com/r/moviepy/>`__ |

MoviePy is the `Python <https://www.python.org/>`__ reference tool for video editing automation! 

It's an open source, MIT-licensed library offering user-friendly video editing 
and manipulation tools for the `Python <https://www.python.org/>`__ programming language.

.. grid:: 1 2 2 2
    :gutter: 4
    :padding: 2 2 0 0
    :class-container: sd-text-center

    .. grid-item-card:: Getting started
        :img-top: _static/medias/index_getting_started.svg
        :class-card: intro-card
        :shadow: md

        New to *MoviePy*? Check out the getting started guides. They contain instructions
        to install *MoviePy* as well as introduction concepts and tutorials.

        +++

        .. button-ref:: getting_started
            :ref-type: ref
            :click-parent:
            :color: secondary
            :expand:

            To the starting guide

    .. grid-item-card::  User guide
        :img-top: _static/medias/index_user_guide.svg
        :class-card: intro-card
        :shadow: md

        The user guide provides in-depth information on the
        key concepts of *MoviePy* with useful background information and explanation.

        +++

        .. button-ref:: user_guide
            :ref-type: ref
            :click-parent:
            :color: secondary
            :expand:

            To the user guide

    .. grid-item-card::  API reference
        :img-top: _static/medias/index_api.svg
        :class-card: intro-card
        :shadow: md

        The reference guide contains a detailed description of
        the *MoviePy* API. The reference describes how the methods work and which parameters can
        be used. It assumes that you have an understanding of the key concepts.

        +++

        .. button-ref:: reference_manual
            :ref-type: ref
            :click-parent:
            :color: secondary
            :expand:

            To the reference guide

    .. grid-item-card::  Developer guide
        :img-top: _static/medias/index_contribute.svg
        :class-card: intro-card
        :shadow: md

        Saw a typo in the documentation? Want to improve
        existing functionalities? The contributing guidelines will guide
        you through the process of improving *MoviePy*.

        +++

        .. button-ref:: developer_guide
            :ref-type: ref
            :click-parent:
            :color: secondary
            :expand:

            To the development guide




Contribute!
--------------

MoviePy is an open source software originally written by Zulko_ and released under the MIT licence. It works on Windows, Mac, and Linux. 

.. raw:: html

    <a href="https://twitter.com/share" class="twitter-share-button"
    data-text="MoviePy - Video editing with Python" data-size="large" data-hashtags="MoviePy">Tweet
    </a>
    <script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';
    if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+'://platform.twitter.com/widgets.js';
    fjs.parentNode.insertBefore(js,fjs);}}(document, 'script', 'twitter-wjs');
    </script>

    <iframe type="text/html" src="https://ghbtns.com/github-btn.html?user=Zulko&repo=moviepy&type=watch&count=true&size=large"
    allowtransparency="true" frameborder="0" scrolling="0" width="152px" height="30px"></iframe>


.. toctree::
    :maxdepth: 3
    :hidden:
    :titlesonly:


    getting_started/index
    user_guide/index
    reference/index
    developer_guide/index


.. _PyPI: https://pypi.python.org/pypi/moviepy
.. _Zulko: https://github.com/Zulko/
.. _Stackoverflow: https://stackoverflow.com/
.. _Github: https://github.com/Zulko/moviepy
.. _Reddit: https://www.reddit.com/r/moviepy/
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
vvfrom moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)vfrom moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
vvfrom moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
from moviepy.editor import *

# Video settings
width, height = 720, 480
duration = 6
bg_color = (245, 245, 245)  # light gray

background = ColorClip(size=(width, height), color=bg_color, duration=duration)

# Load girl character image (transparent PNG)
girl = ImageClip("teen_girl.png").set_duration(duration).resize(height=120)

# Girl walking function: from x=150 to x=450 starting at t=2s
def girl_pos(t):
    if t < 2:
        return (150, height-150)
    elif t <= 4:
        # move to BEWARE elevator over 2 seconds
        x = 150 + (t-2)*(450-150)/2
        return (x, height-150)
    else:
        return (450, height-150)

girl = girl.set_position(girl_pos)

# Create normal elevator (left)
normal_elevator = ColorClip(size=(100, 200), color=(100, 100, 100), duration=duration)
normal_text = TextClip("NORMAL", fontsize=24, color='white', font='Arial-Bold').set_position((160, 230)).set_duration(duration)
normal_elevator = normal_elevator.set_position((150, height-220))

# Create BEWARE elevator (right, hot pink)
beware_elevator = ColorClip(size=(100, 200), color=(255, 105, 180), duration=duration)
beware_text = TextClip("BEWARE", fontsize=24, color='white', font='Arial-Bold').set_position((460, 230)).set_duration(duration)
beware_elevator = beware_elevator.set_position((450, height-220))

# Optional: simple sparkle animation (small white dots)
sparkle = ColorClip(size=(10, 10), color=(255, 255, 255), duration=0.1).set_position((480, 240))
sparkles = [sparkle.set_start(0.5*i).set_end(0.5*i+0.1) for i in range(10)]

# Combine all clips
clips = [background, normal_elevator, normal_text, beware_elevator, beware_text, girl] + sparkles
final = CompositeVideoClip(clips)

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)


# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)


# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)


# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
v

# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)


# Write video
final.write_videofile("girl_chooses_beware_elevator.mp4", fps=24)
