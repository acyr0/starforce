# starforce calculator

This is an analytical starforce calculator for GMS, post-Ignition starforce
costs, based on the math from https://amph.shinyapps.io/starforce.

This came about from a personal desire to have a starforce calculator that was
correct, fast, and up-to-date.
  - Starcatch is 1.05x multiplicative on success chance.
  - MVP discount is multiplicative, and applies on all stars up to and
      including 16* to 17*.
  - Safeguard increases the cost per star by the base cost before any discounts.

If you want to check the math, you can take a look at
[src/lib/calcs.ts](src/lib/calcs.ts).

I don't claim to be an expert on probability or statistics, so its pretty
unlikely that I'll be able to add additional features in that realm. Where the
results here differ from the results you see in other calculators though, I'm
reasonably confident that the results here are correct.

Feel free to open issues in this project if you believe there are any mistakes,
although I can't promise I'll answer them super quickly.

Cary#0001, `aCyr` in GMS Reboot
