Python Speech Recognition
#########################
:date: 2016-09-20 23:26
:author: jmercouris
:category: Software
:slug: python-speech-recognition
:status: published
:description: How to do speech recognition in Python.

The Main Idea
=============

This Program was an exercise in using a Speech API to integrate Speech
recognition into a desktop Python application.

Source: https://github.com/jmercouris/speech_recognition

Screenshot:

|window_sample_text|

Development Story
=================

The first thing I did was I instinctually looked at the Google Cloud API
and signed up for an account. I saw that they had a way to send
audio and get a text response. After ten minutes, I was not able to
discern where the endpoints were, and decided to pursue another avenue.
Google documentation is terrible, and this new product was absolutely no
exception.

In the interests of efficiency, I googled to see whether anyone in the
Python community had already implemented a wrapper or a set of tools,
and it turned out they had, so I simply pip installed their module, ran
the demo, and the demo already satisfied most of the requirements. It
was BSD licensed and could therefore be easily used off the shelf.

The Speech Recognition Library
------------------------------

The great Python library that I used is very aptly called
speech_recogntion.

The project homepage is
here: https://github.com/Uberi/speech_recognition.

As a note of caution, if you are to install on OS X, you should install
PortAudio is a dependency.


.. code-block:: python

    import speech_recognition as sr

    r = sr.Recognizer()
    m = sr.Microphone()

    def record(self):
        # GUI Blocking Audio Capture
        with m as source:
            audio = r.listen(source)

        try:
            # recognize speech using Google Speech Recognition
            value = r.recognize_google(audio)
            self.output = "You said \"{}\"".format(value)
            
        except sr.UnknownValueError:
            self.output = ("Oops! Didn't catch that")
            
        except sr.RequestError as e:
            self.output = ("Uh oh! Couldn't request results from Google Speech Recognition service; {0}".format(e))


Looking at the above code snippet you can see just how easy it is to use
this library. It takes literally seconds to get started with it. No
registering for keys on site, making key pairs, creating separate
threads, etc. It just works. This is how all libraries should be
written.

 The Graphic Library
--------------------

I then decided to combine the example I found with my favorite Python
GUI framework (Kivy) and quickly made an example that included a button,
and an output field (where it would display the result to the user).

Demonstration
=============

Finally, with a few simple lines of code joining everything together, I
was off the ground quickly with a complete demonstration.

.. |window_sample_text| image:: {filename}/images/window_sample_text.png
   :class: pure-img
