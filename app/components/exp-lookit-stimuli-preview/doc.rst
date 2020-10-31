exp-lookit-stimuli-preview
==============================================

Overview
------------------

A frame that to explain any blinding procedures to parents, and offer them the option to preview
stimuli before the study. Two buttons are available to move on: one turns on video recording & shows
the stimuli previews (if the parent wants to preview stimuli), and one moves on to the next frame
that (if the parent declines).

What it looks like
~~~~~~~~~~~~~~~~~~

.. image:: /../images/Exp-lookit-stimuli-preview.png
    :alt: Example screenshot from exp-lookit-stimuli-preview frame

Recording
~~~~~~~~~~

If ``doRecording`` is true, then the family is recorded while previewing stimuli if they choose to.
This is so that if you want to make sure the child didn't see stimuli ahead of the study you can check.

Specifying where files are
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Several of the parameters for this frame can be specified either by providing a list of full URLs and file types, or
by providing just a filename that will be interpreted relative to the ``baseDir``. These are: ``audio``
(``source`` property), ``pauseAudio``, ``unpauseAudio``, ``pauseVideo``, and ``video`` (``source``
property). See the :ref:`expand-assets` tool that this frame uses.

More general functionality
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Below is information specific to this particular frame. There may also be available parameters, events recorded,
and data collected that come from the following more general sources:

- the :ref:`base frame<base frame>` (things all frames do)
- :ref:`video-record`
- :ref:`expand-assets`


Example
----------------

.. code:: javascript

    "my-video-preview": {
        "kind": "exp-lookit-stimuli-preview",
        "doRecording": true,
        "skipButtonText": "Skip preview",
        "previewButtonText": "I'd like to preview the videos",
        "blocks": [
            {
                 "text": "During the videos, we'll ask that you hold your child over your shoulder like this, so that you're facing face away from the screen."
            },
            {
                "image": {
                    "alt": "Father holding child looking over his shoulder",
                    "src": "https://raw.githubusercontent.com/kimberscott/placeholder-stimuli/master/img/OverShoulder.jpg"
                }
            },
            {
                "text": "This is because your child is learning from you all the time, and may pick up on even very small cues about what you think. But if you can't see the stimuli, we're definitely only measuring your child's own beliefs."
            },
            {
                "text": "If you'd like to see the videos your child will be shown, you can take a look ahead of time now. It's important that you preview the videos without your child, so that the videos will still be new to them."
            }
        ],
        "showPreviousButton": true,
        "baseDir": "https://raw.githubusercontent.com/kimberscott/placeholder-stimuli/master/",
        "videoTypes": ["webm", "mp4"],
        "audioTypes": ["mp3", "ogg"],
        "stimuli": [
           {
             "caption": "At the start of each section, we will play a video like this that shows a common household object, like a book or an apple.",
             "video": "cropped_book"
           },
           {
             "caption": "Your child will be looking at images like this, and we'll ask him or her to describe each one.",
             "image": "square.png"
           },
           {
             "caption": "Between sections, we will play audio like this so you know where you are in the study.",
             "audio": "sample_1"
           }
         ]
    }



Parameters
----------------

.. glossary::

    video [Object | ``{}`` ]
        Object describing the video to show. It can have the following properties:

        :source: [String or Array]
            The location of the main video to play. This can be either
            an array of ``{'src': 'https://...', 'type': '...'}`` objects (e.g., to provide both
            webm and mp4 versions at specified URLS) or a single string relative to ``baseDir/<EXT>/``.

    showPreviousButton [Boolean | ``true``]
        Whether to show a 'previous' button

    blocks [Array]
        Array of text blocks to display as an introduction to the preview. Should be a list
        of objects that can be passed to :ref:`exp-text-block`; each can have any of the
        properties below.

    previewButtonText [String | ``'I\'d like to preview the videos'``
        Text on the preview button user clicks to proceed to stimuli/images

    skipButtonText [String | ``'Skip preview'``]
        Text to display on the button to skip the next frame

    stimuli [Array]
        An array of preview stimuli to display within a single frame, defined as an array of objects.
        Generally each item of the list will include ONE of image, video, or audio
        (depending on the stimulus type), plus a caption. Each item can have fields:

        :caption: [String]
            Some text to appear above this video/audio/image
        :video: [String or Array]
            String indicating video URL. This can be relative to baseDir, OR Array of {src: 'url', type: 'MIMEtype'} objects.
        :audio: [String or Array]
            String indicating audio URL. This can be relative to baseDir, OR Array of {src: 'url', type: 'MIMEtype'} objects.
        :image: [String]
            URL of image to display. Can be full path or relative to baseDir/img.

    nextStimulusText [String | ``'Next'``]
        Text on the button to proceed to the next example video/image

    previousStimulusText [String | ``'Previous'``]
        Text on the button to proceed to the previous example video/image

    doRecording [Boolean | ``true``]
        Whether to make a webcam video recording during stimulus preview (begins only if user chooses to preview stimuli). Default true.


Data collected
----------------

No fields are added specifically for this frame type.


Events recorded
----------------

The events recorded specifically by this frame are:

:startPreview: User clicks on start preview button
:nextStimulus: User clicks to move to next stimulus
:previousStimulus: User clicks to move to previous stimulus