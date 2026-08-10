# Misdirection

## Information

- Challenge: [Misdirection](https://play.scriptsorcerers.xyz/challenges#Misdirection-27)
- Category: Crypto
- Description:

```text
Help! Our website got bruteforced. Hopefully the attacker did not leak anything.
```

## Solution

The content of the `enc.txt` file:

```text
1000100010100000100001110100100001010010001010110001101100101010000111000001001001000100101000100100001000101110001
```

Using any tool you like, here I used CyberChef with `Bacon Cipher Decode` and got the string

```text
SCRIPTCTFNOTWHATITSEEMS
```

![alt text](Images/image-2.png)

Remembering that flags all have the form `scriptCTF{...}`, what if I add `{}` to the string above?

```text
SCRIPTCTF{NOTWHATITSEEMS}
```

And it worked!

## Flag

```text
SCRIPTCTF{NOTWHATITSEEMS}
```