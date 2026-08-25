# Trivago

**Author**: carax49<br>
**Date**: 2026-08-23

## Overview

- Category: OSINT
- Description:

```text
Business travel has scaled beautifully this quarter, so much that it has outscaled me! I've been onboarded into so many cities that I woke up with zero situational KPIs and no idea where I am. My points balance is the only sense of self I've got left. Please help me identify the hotel chain!
```

## Analysis

The challenge provides the file `trivago.jpg`, a photo of a hotel room

<img src=./images/trivago.jpg style="border-radius: 3px;">

Since this is a Danish CTF, this hotel is very likely also located in Denmark.

I looked closer at the details in the room, from the painting, the two red and black vases on the table. Especially the pillow with a dragonfly pattern.

This is very likely the hotel's signature pattern

## Solution

Dragonfly in Danish is `guldsmed`. So I tried searching for

```text
guldsmed hotel denmark
```

<img src=./images/image-8.png style="border-radius: 3px;">

And I found the hotel `Guldsmeden Hotel`

Looking through a few photos of this hotel's rooms, I found the style very similar to the room in the challenge's photo

<img src=./images/image-9.png style="border-radius: 3px;">

<img src=./images/image-10.png style="border-radius: 3px;">

## Flag

```text
brunner{Guldsmeden_Hotels}
```