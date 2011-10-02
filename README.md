How to setup local Withings scale data capture
==============================================

This project will allow you to capture scale readings to a local TSV file for 
import into a spreadsheet or other software

Steps
-----

These steps are for my router running DD-WRT, if you're using a different 
network configuration you'll have to modify them appropriately

    1) Copy all bits in this folder to the location you'd like to host from
    2) Run 'mongoose-3.0.exe'
    3) Test service by going to 'http://<YourIpAddress>/info.php' and verify 
       that PHP is functioning 
    4) Redirect all traffic from scalews.withings.com to your computer
      a) Login to DD-WRT on your router
      b) Navigate to 'Administration->Commands'
      c) Add 'iptables -t nat -A PREROUTING -d scalews.withings.net -j DNAT --to <YourIpAddress>' 
         to the commands list
      d) First 'Run Commands' to apply the command immediately
      e) Then 'Save Startup' so that it will be stored for any resets
      f) Then 'Save Firewall' just in case;
    5) Test redirection by going to 'http://scalews.withings.net/cgi-bin/once' 
       and ensure you see only the string '{"status":0,"body":{"once":"21112cb3-1b433eef"}}'
    6) Test scale logging
      a) give it about 20 seconds to send the data after stepping off the scale 
      b) check the measure.tsv file for 'measure' readings

Resources
---------

### Reference sites

* [Withings home page](http://www.withings.com/)
  -- Withings product home page
* [Withings developer forums](http://scaleforum.withings.com/viewforum.php?f=13)
  -- More information here than I expected
* [Withings Scale Hacking](http://www.prolixium.com/mynews?id=915)
  -- I borrowed heavily from this write-up and can't them enough (Local copy saved to .mth file for archival purposes)
* [Body fat formulas](http://www.brianmac.co.uk/fatbia.htm)
  -- How to compute BF from bioelectrical impedance
  
### Tools included with this project

* [Mongoose](http://code.google.com/p/mongoose/)
  -- A very basic, free, stand alone, single exe, zero install webserver
* [PHP](http://php.net/)
  -- PHP script processor 'php-cgi.exe' that is used to run the logging scripts

### Other helpful tools

* [DD-WRT logging](http://www.dd-wrt.com/wiki/index.php/Logging_with_DD-WRT/)
  -- Enable both Services->syslogd(enable) and Security->Log(enable)
* [WallWatcher](http://www.wallwatcher1.com/)
  -- DD-WRT traffic log viewer.  No support but last release still worked great.
* [WireShark](http://www.wireshark.org)
  -- For all your packet sniffing needs

### Other Withing related links

* [Hardwire power](http://www.dellanave.com/blog/2010/02/19/add-a-power-adapter-to-your-withings-scale/)
  -- Might look into this simple mod if it starts eating batteries