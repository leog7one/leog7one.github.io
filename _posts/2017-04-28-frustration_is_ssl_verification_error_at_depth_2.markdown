---
layout: post
title:  "Frustration is.. SSL verification error at depth 2"
date:   2017-04-27 22:30:31 -0400
---


How to fix: ‘SSL verification error at depth 2’ for Ruby Gem Install

![](https://cdn-images-1.medium.com/max/800/1*jfp0rEDf9neoIIcPNq26bA.jpeg)

I was working on a follow along on how to create rspec to test a ruby file.
So when I went to run:

`rspec --init `

to create the new files. I received an error that the command was not found.
So I figured I needed to install the gem on the computer.I have installed gems before so I knew how easy this should be. Boy… was I wrong this time.
I went ahead and went to Rubygems.org and copied the install command:

`gem install rspec`

Then I went ahead and pasted it into my Terminal.

I then got this error:

```
ERROR: SSL verification error at depth 2: certificate has expired (10)
ERROR: Certificate /C=BE/O=GlobalSign nv-sa/OU=Root CA/CN=GlobalSign Root CA expired at 2014–01–28T12:00:00Z
ERROR: SSL verification error at depth 2: certificate has expired (10)
ERROR: Certificate /C=BE/O=GlobalSign nv-sa/OU=Root CA/CN=GlobalSign Root CA expired at 2014–01–28T12:00:00Z
ERROR: SSL verification error at depth 2: certificate has expired (10)
ERROR: Certificate /C=BE/O=GlobalSign nv-sa/OU=Root CA/CN=GlobalSign Root CA expired at 2014–01–28T12:00:00Z
ERROR: Could not find a valid gem ‘rspec’ (>= 0), here is why:
Unable to download data from https://rubygems.org/ — SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://api.rubygems.org/specs.4.8.gz)
ERROR: SSL verification error at depth 2: certificate has expired (10)
ERROR: Certificate /C=BE/O=GlobalSign nv-sa/OU=Root CA/CN=GlobalSign Root CA expired at 2014–01–28T12:00:00Z
```


Here is where it got interesting. I looked at multiple sources to try to fix my issues, here is just a few:

[https://rvm.io/support/fixing-broken-ssl-certificates](https://rvm.io/support/fixing-broken-ssl-certificates)

[https://stackoverflow.com/questions/11149623/where-can-i-find-ssl-certificates-on-mac-osx](https://stackoverflow.com/questions/11149623/where-can-i-find-ssl-certificates-on-mac-osx)

[https://stackoverflow.com/questions/40029184/cannot-install-any-ruby-gems-on-mac-os-ssl-connect-error](https://stackoverflow.com/questions/40029184/cannot-install-any-ruby-gems-on-mac-os-ssl-connect-error)

[http://help.rubygems.org/discussions/problems/22983-ssl-server-certificate-verify-failed#comment_41050585](http://help.rubygems.org/discussions/problems/22983-ssl-server-certificate-verify-failed#comment_41050585)

I first ran:

`rvm osx-ssl-certs update all`

and it stated the files were up to date!

I checked the keychain and did not find any expired certs as to what the problem stated it was.

I went ahead and tried running a tool that was made for ruby to try and find a more detailed explanation as to why it was failing. It is called ‘doctor.rb’
[https://github.com/mislav/ssl-tools/blob/master/doctor.rb](https://github.com/mislav/ssl-tools/blob/master/doctor.rb)

After running this it stated that the folder with the cert was empty.

This I found weird because when I ran a manual search for the cert I did get a result of 1 cert.. hhmmmmm….
So I figured that maybe the cert needs to be in 2 places!

From more reading, I came to a conclusion that 2 different folders were being referenced in the different solutions..
```
/etc/openssl/cert.pem
/usr/local/etc/openssl/cert.pem
```

So I decided to find these folders. To look into the folders you have to go directly to them using ‘`Go to Folder`’ in Finder.
When I placed the whole search path in the 1st one:

`/etc/openssl/cert.pem`

It came back with a result of ‘The file cannot be found’
So I tried just searching up the folder and noticed the file was not there!

I then search the other folder

`/usr/local/etc/openssl/`

and found a cert.pem file there!

This would explain why the ‘doctor.rb’ tool said the folder was empty but a terminal search did show one on the computer.
Keep in mind the first thing I did before all this was run:

`rvm osx-ssl-certs update all`

and when I first ran this it stated that the files were up to date, but they really weren’t!

I went ahead and deleted the cert.perm file from `/usr/local/etc/openssl/`
then went ahead and ran

`rvm osx-ssl-certs update all` again.

This time it showed the folder path and file were updated!

I then went ahead and ran the gem install again:

`gem install rspec` and it installed!

So in a nutshell:
1. Go to `/etc/openssl/` , if there is a cert.pem file there, delete it. If there is no cert.pem file do nothing.

2. Go to `/usr/local/etc/openssl/` , if there is a cert.pem file there, delete it, If there is no cert.pem there do nothing.

3. Go to terminal and run `rvm osx-ssl-certs update all`

4. Terminal should output that the files in both locations have been updated.

![](https://cdn-images-1.medium.com/max/800/1*sHXeNpkk41igS1-NjDlOtA.jpeg)

Now run your Gem Install and rejoice in victory!!
