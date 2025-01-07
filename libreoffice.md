Build on Linux
--------------

https://wiki.documentfoundation.org/Development/BuildingOnLinux


Build on Windows
----------------


Build on macOS
----------------


UNO API
-------

Block/Non-block

[createSystemChild](https://api.libreoffice.org/docs/idl/ref/interfacecom_1_1sun_1_1star_1_1awt_1_1XSystemChildFactory.html)

[OpenOffice Forum: xSystemChildFactory->createSystemChild() hangs](https://forum.openoffice.org/en/forum/viewtopic.php?t=10430)

[createSystemChild and createWindow hang on Windows trying to create a child window
](https://www.mail-archive.com/dev@openoffice.org/msg02961.html)


Module AVMedia
--------------


Module Slideshow
----------------


Repair Package
--------------


Convert to PDF (soffice)
------------------------

``` bash
soffice --headless --invisible --convert-to pdf /tmp/broken.pptx --outdir /tmp/out
```