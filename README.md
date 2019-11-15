# F5 NGINX Tech day lab files for Aug. 5th 2019

This is a very simple lab I created from several different sources.  It is intended to be a simple quick into to nginx

Everythign we do in linux will need sudo at the front

In the following labs commands and code are in blocks

`commands like this`


>     code like this
>     second line of code


if using UDF a simple unbuntu 18.04 linux - desktop - 1 core 1gb ram should suffice == mini?
- it should have openssl and ssh installed already, jump right into updating and installing nginx

It is easiest to setup ssh keys and ssh from local machine to UDF instance

https://github.com/trimstray/nginx-admins-handbook

The best place to run these labs is probably via the "hello-world" docker image
- Using docker, run "docker run hello-world" and it should download and run the nginx docker image to display a default web page.

Then I recommend using VSCode and the Remote-Docker extension.  This extension allows you to connect to a local docker container and code within vscode in that container.  Everything in a nice little package.

Or just run the hello-world docker image in interactive mode (attached bash) and lab away!

Please open an issue for any problems, RFEs or questions.  NJOY!!!
