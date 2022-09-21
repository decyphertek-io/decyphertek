Mycroft-ai
=====

Mycroft is an open source TTS engine and voice assitant that focuses privacy. Alternatives to popular voice assistants.  


Install
-------

    $ cd ~/
    $ git clone https://github.com/MycroftAI/mycroft-core.git
    $ cd mycroft-core
    $ bash dev_setup.sh

    usage: start-mycroft.sh [command] [params]

    Services:
      all                      runs core services: bus, audio, skills, voice
      debug                    runs core services, then starts the CLI

    Services:
      audio                    the audio playback service
      bus                      the messagebus service
      skills                   the skill service
      voice                    voice capture service
      wifi                     wifi setup service
      enclosure                mark_1 enclosure service

    Tools:
      cli                      the Command Line Interface
      unittest                 run mycroft-core unit tests

    Utils:
      skill_container <skill>  container for running a single skill
      audiotest                attempt simple audio validation
      audioaccuracytest        more complex audio validation
      sdkdoc                   generate sdk documentation

    Examples:
      $ start-mycroft.sh all
      $ start-mycroft.sh cli
      $ start-mycroft.sh unittest
      

References
----------

    https://mycroft.ai/
    https://market.mycroft.ai/skills
    https://github.com/MycroftAI?utf8=%E2%9C%93&q=android&type=&language=
