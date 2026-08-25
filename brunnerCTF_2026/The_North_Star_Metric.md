# The North Star Metric

**Author**: carax49<br>
**Date**: 2026-08-23

## Overview

- Category: OSINT
- Description:

```text
My manager says Brunnerne Inc. needs a North Star Metric (NSM) to serve as a guiding light for the company. After some extensive field research, I found what appears to be a rather mature implementation with a proven track record of keeping people on course.

As part of my research, I need answers for the following questions:

    1. What is the name of the lighthouse?
    2. What is inside the tub at the bottom of the building?
    3. Who was the lighthouse keeper in 1930 (full name)?

Flag Format: brunner{<lighthouse_name>,<tub_contents>,<lighthouse_keeper_in_1930>} (the three answers written in lowercase with underscores instead of spaces, separated by commas, and all wrapped in brunner{}).
Example: If you found the lighthouse "Agersø Fyr" with a tub full of "Brunsviger" who had the lighthouse keeper "Jan Bruun Sviger", the flag would be brunner{agersø_fyr,brunsviger,jan_bruun_sviger}
```

## Analysis

The challenge provides an image `north-star.jpg` showing a lighthouse

<img src=./images/north-star.jpg style="border-radius: 3px;">

The task is to answer 3 questions:

```text
1. What is the name of the lighthouse?
2. What is inside the tub at the bottom of the building?
3. Who was the lighthouse keeper in 1930 (full name)?
```

## Solution

I dropped the image into `Google Lens` and immediately learned it was the lighthouse `Lyngvig`, or `Lyngvig Fyr` in Danish

<img src=./images/image-11.png style="border-radius: 3px;">

After a bit of searching, I found the following page

```text
https://fyrtaarne.dk/?lh=188
```

<img src=./images/image-12.png style="border-radius: 3px;">

As we can see, `Ejler Haubrik` served as Lighthouse master from 1927 to 1933, so the answer to question 3 is very likely `Ejler Haubrik`

And to answer question 2, in this [video](), at 04:42, we can clearly see it's sand

<img src=./images/image-13.png style="border-radius: 3px;">

From here, we have the answers to all 3 questions

```text
1. Lyngvig Fyr
2. Sand
3. Ejler Haubirk
```

## Flag

```text
brunner{lyngvig_fyr,sand,ejler_haubirk}
```