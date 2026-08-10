# Midnight Snack

## Information

- Challenge: [Midnight Snack](https://play.scriptsorcerers.xyz/challenges#Midnight%20Snack-31)
- Category: Geo-OSINT
- Description:
```text
Can you find the address of this Taco Bell? Example: scriptCTF{1337_Orange_St}
```

## Solution

The challenge gives me an image called `tacobell.png`.

![alt text](Images/tacobell.png)

The picture shows a Taco Bell menu board, and on the right side of the image, hidden in the dark area, is the word `Parmer`.

I searched on Google and found 3 Taco Bell branches on Parmer Lane.

![alt text](Images/image-8.png)

After checking all 3, the one that matched best was the branch at `9900 Parmer Lane`.

![alt text](Images/image-9.png)

![alt text](Images/image-10.png)

You can see the full view at

```url
https://maps.app.goo.gl/phHMekdg2CNCHR9i6
```

## Flag

```text
scriptCTF{9900_W_Parmer_Ln}
```