sslv3checker
============

Python script to check if a website supports SSLv3.

*Syntax*:

`sslv3checker.py {file}`

*Inputs:*

>The optional {file} parameter points to a file containing a list of hosts and IPs. If not specified, the default file './target\_lists' is used.

>An example of the file contents might be:

    # a URL
    https://1.2.3.4/
    # IP on its own
    1.2.3.4
    # Specify a port
    1.2.3.4:8443

*Caveats*

>For speed of execution, the program forks a copy of itself for every line in the data file. There is no mechanism in place to limit how many instances are spawned, so if you use a long list of hostnames you do so at your own risk. Better still, why not fork the project, write the code to limit the program to max\_forks, and submit it back to me as a patch? I'd appreciate that ;-)

>Error checking on the hostnames is pretty basic, but for the most part effective.

>I am not a python programmer. Please forgive the inevitable style failures and general "Ugh, you just don't do it that way" issues; this is pretty much my first script, so I would be grateful for a little slack. Ok, a lot.

*Author*

John Herbert  ::  @mrtugs  ::  http://lamejournal.com/
