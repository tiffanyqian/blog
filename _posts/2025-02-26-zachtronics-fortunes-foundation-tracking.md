---
title: "Zachtronics Fortune's Foundation - Data Collection"
tags:
    - bigdata
---

As you all know, I love solitaire and minesweeper so much that my favorite games are modified versions of them. Zachtronics has a bunch of solitaire variants, and one of my favorites is Fortune's Foundation. It's "fortress style solitaire" that has another suit made of the Major Arcana tarot cards. I call it tarot solitaire!

This may not make much sense if you've never played, but I'll try to explain the important points to know for this data collection I've been doing. The tarot cards ranging from 0 to 21 are their own special suit, and notably they can only stack from 0 or from 21. Whatever tarot card is the last card that gets put up into the stack is the "reading" that you get from that game. Super cute. After a while of playing, I started wondering if there was any pattern to the tarot cards you can win with. My initial theory was that the card wins would result in a Bimodal distribution due to 0 and 21 being the starting points. However, because of the challenge, I know that I sometimes try to go for as close to 0 and 21 as possible... thus, data tracking of wins to see if there actually is a pattern or if it can be affected by play style.

I started tracking my tarot solitaire wins around October 2024. As of 02/26/25, the win spread looks like this:
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/zachtronics_ff_wins.png" alt="Zachtronics Fortune's Foundation Wins 02/26/25">

As of right now I'm not seeing much. As expected, 0 and 21 aren't as low as expected because I enjoy trying to make myself go for them. This will be updated with further wins, and perhaps even collected data from other friends that are willing to indulge me.