Internet In A Box
=================

"Internet-in-a-Box “learning hotspots” are used in dozens of countries, to give everyone a chance."

Install
-------

    # To install IIAB 8.0 Preview 3 from 2022-08-20: ( Requires Raspberry Pi & a computer to write SD card )
    1. Install Raspberry Pi Imager onto your favorite Windows, macOS, or Linux computer.
    # If your computer doesn't have a slot for SD cards, put your microSD card in a microSD card reader (typically $5-10).
    2. Run rpi-imager --repo http://iiab.io/fast.json
        Click CHOOSE OS to pick an IIAB image.
        See IIAB Image Choices (table below) if you want more details on each image.
        Click CHOOSE STORAGE to specify which microSD card it should write to.
        Click WRITE to begin!
    3. After the image has been written onto the microSD card — eject and remove the card from your Windows, macOS, or Linux computer.
    4. Insert the microSD card into any recent model Raspberry Pi and turn it on!
    5. If you chose Raspberry Pi OS with desktop and have a screen attached, a browser should open automatically in about two minutes, showing your IIAB home page: http://box.lan
    6. Use a laptop to connect to WiFi network Internet in a Box.
    7. Open your laptop's browser to: http://box.lan
    8. In the above doesn't work, try: http://10.10.10.10 (or http://172.18.96.1, if image pre-dates July 2022)
    9. If your laptop is a Mac or Linux, run the command ssh iiab-admin@box.lan to log in to the Raspberry Pi.
        The username is iiab-admin and the password is g0adm1n
        If your laptop is Windows, install an ssh program (like putty) to do the same thing (log in to box.lan).
    10. To change your iiab-admin password on the Raspberry Pi, run the command: passwd
    11. The root filesystem will expand to use your full microSD card or HDD/SSD drive (this can take several minutes!) but you may need to reboot Raspberry Pi OS to make this happen. PR #3336
    12. Finally, use IIAB's browser-based Admin Console to add content for your school or community!

References
----------

    https://internet-in-a-box.org/