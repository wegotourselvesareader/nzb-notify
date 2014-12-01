Notify Processing Script
========================
This script was intended to be an [NZBGet](http://nzbget.net) _post-processing_
wrapper to different forms of notification services.

NZBGet users can be notified on supported devices of the status of a download
they made.  Non-NZBGet users can also use this tool as a standalone app that
can message their devices as they please.

Installation Instructions
=========================
1. Ensure you have at least Python v2.6 or higher installed onto your system.
2. Simply place the __Notify.py__ and __Notify__ directory together.
   * __NZBGet users__: you'll want to place these inside of your _nzbget/scripts_ directory. Please ensure you are running _(at least)_ NZBGet v11.0 or higher. You can acquire the latest version of of it from [here](http://nzbget.net/download).

The Non-NZBGet users can also use this script from the command line.
See the __Command Line__ section below for more instructions on how to do this.

**Note:** The _Notify_ directory provides all of the nessisary dependencies
in order for this script to work correctly. The directory is only required
if you do not have the packages already available to your global
environment. These dependant packages are all identified under the
_Dependencies_ section below.

Supported Notify Services
=========================
The table below identifies the provider _Notify.py_ supports and the
location that content is retrieved from.

| Notification Service | Service ID | Default Port | Example Syntax |
| -------------------- | ---------- | ------------ | -------------- |
| [Boxcar](https://boxcar.io/)  | boxcar://   | (TCP) 443   | boxcar://hostname<br />boxcar://hostname/@tag<br/>boxcar://hostname/device_token<br />boxcar://hostname/device_token1/device_token2/device_tokenN<br />boxcar://hostname/alias<br />boxcar://hostname/@tag/@tag2/alias/device_token
| [Growl](http://growl.info/)  | growl://   | (UDP) 9887   | growl://hostname<br />growl://hostname:portno
| [Faast](http://faast.io/) | faast://    | (TCP) 443    | faast://authorizationtoken
| JSON (Simple)        | json:// or jsons://   | (TCP) 80 or 443 | json://hostname<br />json://user@hostname<br />json://user:password@hostname:port<br />json://hostname/a/path/to/post/to
| [KODI](http://kodi.tv/) | kodi:// or kodis://    | (TCP) 8080 or 443   | kodi://hostname<br />kodi://user@hostname<br />kodi://user:password@hostname:port
| [Notify My Android](http://www.notifymyandroid.com/) | nma://   | (TCP) 443    | nma://apikey
| [Prowl](http://www.prowlapp.com/) | prowl://   | (TCP) 443    | prowl://apikey<br />prowl://apikey/providerkey
| [Pushalot](https://pushalot.com/) | palot://    | (TCP) 443    | palot://authorizationtoken
| [PushBullet](https://www.pushbullet.com/) | pbul://    | (TCP) 443    | pbul://accesstoken<br />pbul://accesstoken/#channel<br/>pbul://accesstoken/A_DEVICE_ID<br />pbul://accesstoken/email@address.com<br />pbul://accesstoken/#channel/#channel2/email@address.net/DEVICE
| [Pushover](https://pushover.net/)  | pover://   | (TCP) 443   | pover://user@token<br />pover://user@token/DEVICE<br />pover://user@token/DEVICE1/DEVICE2/DEVICEN<br />_Note: you must specify both your user_id and token_
| [Toasty](http://api.supertoasty.com/)  | toasty://   | (TCP) 80   | toasty://user@DEVICE<br />toasty://user@DEVICE1/DEVICE2/DEVICEN<br />_Note: you must specify both your user_id and at least 1 device!_
| [XBMC](http://kodi.tv/) | xbmc:// or xbmcs://    | (TCP) 8080 or 443   | xbmc://hostname<br />xbmc://user@hostname<br />xbmc://user:password@hostname:port
| XML (Simple)        | xml:// or xmls://   | (TCP) 80 or 443 | xml://hostname<br />xml://user@hostname<br />xml://user:password@hostname:port<br />xml://hostname/a/path/to/post/to

Dependencies
============
The following dependencies are already provided for you within the
_Notify_ directory and no further effort is required by you. However, it
should be known that Notify.py depends on the following packages:

| Name                         | Version | Source                                                                               |
| ---------------------------- |:------- |:------------------------------------------------------------------------------------ |
| backports-ssl_match_hostname | 3.4.0.2 | https://pypi.python.org/pypi/backports.ssl_match_hostname/3.4.0.2                    |
| chardet                      | 2.2.1   | https://pypi.python.org/pypi/chardet/2.2.1                                           |
| ndg-httpsclient              | 0.3.2   | https://pypi.python.org/pypi/ndg-httpsclient/0.3.2                                   |
| ordereddict                  | 1.1     | https://pypi.python.org/pypi/ordereddict/1.1                                         |
| pynzbget                     | 0.2.1   | https://pypi.python.org/pypi/pynzbget/0.2.1                                          |
| requests **[P]**             | 2.3.0   | https://pypi.python.org/pypi/requests/2.3.0                                          |
| six                          | 1.6.1   | https://pypi.python.org/pypi/six/1.6.1                                               |
| pyasn1                       | 0.1.7   | https://pypi.python.org/pypi/pyasn1/0.1.7                                            |
| pyOpenSSL **[P]**            | 0.14    | https://pypi.python.org/pypi/pyOpenSSL/0.14                                          |
| netgrowl                     | 0.6.3   | http://the.taoofmac.com/                                                             |
| urllib3 **[P]**              | 1.9     | https://pypi.python.org/pypi/urllib3/1.9                                             |

**Note:** The items above denoted with a **[P]** were patched in efforts to:
- Make their libaries compatible with Python v2.6.
- Fix bugs to add stability to the overall functionality.
- Add the nessesary enhancments that benifit this wrapper tool.

To be as transparent as possible, all patches have been provided in the
[_/patches_](https://github.com/caronc/nzbget-notify/tree/master/patches) directory.

Command Line
============
Notify.py has a built in command line interface that can be easily tied
to a cron entry or can be easilly called from the command line to automate
the fetching of subtitles.

Here are the switches available to you:
```
Usage: Notify.py [options]

Options:
  -h, --help            show this help message and exit
  -s URL(s), --servers=URL(s)
                        Specify 1 or more servers in their URL format ie:
                        growl://mypass@localhost
  -t TITLE, --title=TITLE
                        Specify the title of the notification message.
  -b BODY, --body=BODY  Specify the body of the notification message.
  -i, --include_image   Include image in message if the protocol supports it.
  -L FILE, --logfile=FILE
                        Send output to the specified logfile instead of
                        stdout.
  -D, --debug           Debug Mode
```

Here is simple example:
```bash
# Send a notification to XBMC (assuming its listening on
# port 8080 at the ip 192.168.0.2 with respect to the example
# below:
python Notify.py -s xbmc://192.168.0.2 -t "Hello" -b "World!"

# you can also use it's new name (kodi) to achive the same
# results:
python Notify.py -s kodi://192.168.0.2 -t "Hello" -b "World!"
```

You can also mix and match as many servers as you want by separating
your urls with a comma and/or space.
```bash
# Send a notification to XBMC and a Growl Server
python Notify.py \
    -s growl://192.168.0.10,xbmc://user:pass@192.168.0.2 \
    -t "Hello" -b "World!"
```
