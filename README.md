sslv3checker
============

Python script to check if a website supports SSLv3. This is considered to be A Bad Thing and will return "XX" if an SSLv3 connection is successful.

##Syntax##

`sslv3checker.py [file]`

##Inputs##

>The optional [file] parameter points to a file containing a list of hosts and IPs. If not specified, the default file './target\_lists' is used.

>An example of the file contents might be:

    # a URL
    https://1.2.3.4/
    # IP on its own
    1.2.3.4
    # Specify a port
    1.2.3.4:8443

> It is generally better to use IPs than hostnames, as it is more likely to avoid redirects and similar that might lead to a ?? result (see below).

##Output##

>Output is pretty straightforward but can be quite wide, as the raw error codes are included (or in the case of SSLv3 connections, the accepted ciphers).

>Response codes are:

     XX - site supports SSLv3 (bad donkey!)
        - site rejected SSLv3 (yay!)
     ?? - some other error occurred. I haven't dug into what the error is.


>Here's a sample output that is also timed:

    sslv3#  time python sslv3.py
    Checking hosts for SSLv3:
                     www.lamejournal.com:443:     Exception: [Errno 1] _ssl.c:504: error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure
                 www.informationweek.com:443:     Exception: [Errno 1] _ssl.c:504: error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure
                          www.google.com:443:  XX ('RC4-SHA', 'TLSv1/SSLv3', 128)
                           www.yahoo.com:443:  XX ('RC4-SHA', 'TLSv1/SSLv3', 128)
                       www.microsoft.com:443:  XX ('RC4-MD5', 'TLSv1/SSLv3', 128)
    Done
    
    python sslv3.py  0.02s user 0.02s system 15% cpu 0.284 total

> So we're looking at less than 0.3 seconds to check 5 web sites on the Internet.

##Caveats##

>For speed of execution, the program forks a copy of itself for every line in the data file. There is no mechanism in place to limit how many instances are spawned, so if you use a long list of hostnames you do so at your own risk. Better still, why not fork the project, write the code to limit the program to max\_forks, and submit it back to me as a patch? I'd appreciate that ;-)

> Output order is based on when the process forked and how quickly the website responded. It's not controlled

>Error checking on the hostnames is pretty basic, but for the most part effective.

>"Other error" handling is lame in the extreme

>I am not a python programmer. Please forgive the inevitable style failures and general "Ugh, you just don't do it that way" issues; this is pretty much my first script, so I would be grateful for a little slack. Ok, a lot.

##Author##

John Herbert  ::  @mrtugs  ::  http://lamejournal.com/

