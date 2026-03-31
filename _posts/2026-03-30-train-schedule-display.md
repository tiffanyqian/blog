---
title: "Train Schedule Display Project!"
breadcrumbs: true
tags:
    - project
    - coding
    - transit
---

public transportation lovers wya!!

Here's my process-ramble / semi-tutorial on a SF MUNI and Caltrain schedule display! Spoiler: this project functions but is still a WIP. My general inspiration was the schedule displays at train/bus stops as decor. I was also motivated by the fact that my morning commute varied wildly depending on bus delays... I had multiple routes to get to work and every morning I'd have to check transit multiple times to see when I'd have to leave and which bus had the best transfer. Annoying! Thus, train schedule display: two birds fixed with one API request!
#### Hardware
There were a lot of LED displays that I looked at, but I ended up ordering an [Adafruit MatrixPortal kit](https://www.adafruit.com/product/4745?srsltid=AfmBOoqwtRpDSj4NJvido4vmpxAwRZZqTwkYBUnV2wESGgkPBtI68oB-) to save myself some time on misc. hardware issues and soldering time. There are some cons to this that I'll get into later- but overall the convenience got me started on the project much sooner than if I had to do all the wiring by myself.
#### Code
This was baby's first API request foray!! I used [511 Open Data](https://511.org/open-data/transit) to make my API calls. I believe this is what literally everyone uses, even SFMTA, and you can get a free API token to make 60 requests per 3600 seconds (AKA 1 call every minute). The data exchange protocol is documented pretty well [here](https://511.org/media/407/show).

I decided to code on the MatrixPortal with CircuitPython since I've been doing much more in Python than C++ lately. I spent a while just figuring out the basics of API requesting and parsing JSON into what I needed in VS Code. I ended up writing a wrapper function to make API requests for specific transit agency / stop IDs.

There were some difficulties transferring my code onto the MatrixPortal... I had never used CircuitPython before and didn't realize how restrictive it was. The first major problem was that the 511 API gave me data with a SIRI format that freaked out typical JSON unpackers. The way I had been parsing it on my computer didn't work on the M4 processor, but I did manage to find a workaround that was slightly bulkier. Surely that won't cause any problems!

I used a lot of the [Adafruit CircuitPython tutorials](https://learn.adafruit.com/rgb-led-matrices-matrix-panels-with-circuitpython/matrixportal) and [CircuitPython Core Module References](https://docs.circuitpython.org/en/latest/shared-bindings/displayio/) to get the screen connected and code translated. The layout process wasn't anything super crazy- mostly following documentation, making point changes, and displaying changes to the screen until I was satisfied. Bitmap Label is what I used for all the text displayed.
#### Errors & Future Updates

I had a lot of ambitions and had a lot of them shot down due to hardware or software limitations. Sucks, but that's life. Here are some of my grievances and future to-dos:
- The colors didn't match as closely as I wanted to, unavoidable unfortunately.
- I wanted to have scrolling images or other fun things in-between the MUNI and Caltrain screens using a BitMap pixel drawing, but I ran into memory issues with that... so it was scrapped (for now).
- I wanted to implement an overnight shut-off that would, based on call request time, stop making requests between 1 AM and 6 AM (since MUNI / Caltrain doesn't run during this time ) unless a side button was pressed. This semi-works, but fails here and there and I need to do some further debugging.
- Memory. Fragmentation. Issues. Galore. This is due to the workaround to the SIRI JSON format from the 511 API creating crazy chunks of data, and apparently CIRCUITPYTHON LABEL REALLOCATES THE LABEL'S MEMORY EVERY TIME THE TEXT IN THE LABEL IS UPDATED. HELLO? THAT IS SOOOO STUPID. THE TEXT CHANGES EVERY MINUTE FOR 3 DIFFERENT THINGS???
	- This means the code fragments after a while and the program stops. It will rerun just fine if you reboot it, but that's why this project is a WIP still.
	- You can read more about this memory error on the Adafruit website [here](https://learn.adafruit.com/memory-saving-tips-for-circuitpython/reducing-memory-fragmentation) as it seems to be a pretty known issue. I've tried pretty much every single fix mentioned at the above link other than manually assigning chunks of data for each variable. Sadly, that'll probably what I have to do in the future to fully fix this.
#### Final Thoughts / Product
Currently, the code is in a weird position. It runs just fine, but may need to be restarted every once in a while due to memory allocation weirdness. Blargh. I'll turn it occasionally when I have people over and they need to take the bus, and it still looks pretty cool:

\[ insert image here ]

Here's the generic code / link to it- good luck!