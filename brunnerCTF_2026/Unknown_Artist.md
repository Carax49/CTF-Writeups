# Unknown Artist

**Author**: carax49<br>
**Date**: 2026-08-23

## Overview

- Category: OSINT
- Description:

```text
An unknown artist at Brunnerne has been creating some music. The artist has been using a secret platform to hide a flag. Can you find it?
```

## Analysis

The challenge provides the file `Brunnerne Inc.mp3`. I checked the file's metadata with `exiftool`

```text
...

Title                           : Brunnerne Inc
Source URL                      : https://suno.com/song/b408fe76-c81f-4a96-b10e-b9df4e5d4ec2

...
```

And I found a URL in the metadata

## Solution

Accessing the URL above led me to the page where the artist posted this track

<img src=./images/image-6.png style="border-radius: 3px;">

And right in front of me was a base64 string

```text
YnJ1bm5lcntmcg==
```

Visiting the artist's profile, I saw a total of 4 tracks

<img src=./images/image-7.png style="border-radius: 3px;">

And similarly, visiting each of those tracks, I found one more base64 string per track

```text
YnJ1bm5lcntmcg==
MG1fbTM3NGQ0Nw==
NF83MF81M2NyMw==
N181MG45fQ==
```

And decoding those 4 strings gave me:

```text
brunner{fr
0m_m374d47
4_70_53cr3
7_50n9}
```

## Flag

```text
brunner{fr0m_m374d474_70_53cr37_50n9}
```