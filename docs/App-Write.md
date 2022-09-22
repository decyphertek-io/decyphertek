App Write
=====

Secure Open-Source Backend Server for Web, Mobile & Flutter Developers.

Docker Install
--------------

     $ docker run -it --rm \ --volume /var/run/docker.sock:/var/run/docker.sock \ --volume "$(pwd)"/appwrite:/usr/src/code/appwrite:rw \ --entrypoint="install" \ appwrite/appwrite:0.15.3

Node JS Install
----------------

     $ npm install node-appwrite --save


References
----------

https://appwrite.io/?utm_source=website&utm_medium=javascript&utm_campaign=Libhunt