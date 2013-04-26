Dynamic PCAP play patch for SIPp
=======================

This patch allows [SIPp](http://sipp.sourceforge.net/) to replay the same PCAP file of an RTP capture. Normally, RTP clients will reject packets that have the same Sequence number and/or a wrong Timestamp.

It helps in building SIPp scenarios that involve many PCAP playback operations to be built more easily.

One such case would be testing an application that involves multiple DTMF playbacks with the same digit. Without the patch, you would need to create as many ordered DTMF PCAPs as you need in the scenario, instead of repeating the same.

The patch adds a new exec action to SIPp named "play\_dyn\_pcap\_audio", to be used as follows.

```xml
<action>
  <exec play_dyn_pcap_audio="pcap/dtmf_2833_4.pcap"/>
</action>
```

Applying the patch
------------------
The patch has been applied and confimed working on SIPp stable v3.3 and on SVN checkouts from the same period.

It is applied (on OSX) using
```
patch -p1 -i /path/to/sipp_support_dynamic_pcap_play.diff
```
from inside the SIPp source tree.

History
-------

This patch originated on [this mailing list post](http://permalink.gmane.org/gmane.comp.telephony.sipp.user/5751) and was created by Giulliano Paes Carnielli.

I created this repository because the patch is very useful and has apparently never been added to SIPp. The mailing list archive is there but the patch has disappeared.

This is the original mailing list post:

> De: Giulliano Paes Carnielli 
> 
> Enviada em: segunda-feira, 21 de novembro de 2011 12:45
> 
> Para: 'sipp-users <at> lists.sourceforge.net'
> 
> Assunto: [Contribution] Support for dynamic PCAP play (play the same PCAP multiple times)
> 
> Hello,
> 
> The SIPP tool is being used in my project for long (despite, I'm personally new to the tool). But in a recent
> development I've faced a limitation of the tool that seems to be recurring. Actually, I've searched
> forums and mailing lists, trying to find a solution. But I've noticed that other people also have the same problem.
> 
> Currently, you can use the SIPP to play a PCAP file to simulate a DTMF signal, sent over RTP. However, I've hit
> a scenario where I need to play multiple times the same PCAP file. That operation is not correctly
> supported because the PCAP file is simple sent as it is and, therefore, errors are raised because all RTP
> packets end up with the same Sequence Number / Timestamp.
> 
> I've coded a fix for this problem that fitted quite well for the needs of my project and, as I found other
> people with the same problem, I've decided to submit my changes to your review.
> 
> Remarks:
> 1. I didn't changed any existing functionality of the tool. Thus, this change is totally backward compatible
> 2. I've included a new exec action called "play\_dyn\_pcap\_audio", which will do the trick
> 3. The new action will dynamically change the Sequence Number and Timestamp of the RTP packets sent
> 4. Possibly, the same trick would be applied to the "play\_pcap\_video" (it wasn't my objective, so I didn't
> that yet)
> 
> Please, let me know your comments. This is the first time I contribute for an opensource tool, so it is
> possible that I've used wrong code standard or naming conventions. Additionally, despite I'm a user of
> the SIPP tool, I have only a superficial knowledge about SIP/RTP protocols. Therefore, it would be great
> any feedback from you.
> 
> Regards,

> Giulliano Paes Carnielli, Senior Developer and Technical Leader 

Attribution
-----------

I (Luca Pradovera) do not claim any attribution of the patch or contained code. This repository was created mainly because the patch is so useful for everyday testing.

All contained code was, as far as I know, created by Giulliano Paes Carnielli.
