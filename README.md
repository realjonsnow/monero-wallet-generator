# monero-wallet-generator
Monero/Aeon offline wallet generator

This page generates a new Monero or Aeon address.
It is self contained and does all the necessary calculations locally,
so is suitable for generating a new wallet on a machine that is not connected to the network,
and may even never be. This way, you can create a Monero or Aeon wallet without risking the keys.

The repository contains 3 different editions:

- [Original moneromooo's wallet generator](https://jollymort.github.io/monero-wallet-generator/monero-wallet-generator.html)
- [Dice (d6) version of the wallet generator](https://jollymort.github.io/monero-wallet-generator/monero-wallet-generator-d6.html)
- [Printable version of the wallet generator](https://jollymort.github.io/monero-wallet-generator/monero-wallet-generator-print.html)

## Dice (d6) Version Notes

I wanted a way to generate a Monero wallet from dice (d6) rolls.
Previously I did it by rolling d6 triplets and converting the resulting number (0-216) to a 2-digit base16 number (00 to D8).
Repeat enough times, and you get the 64 char base16 string which can be used as seed and generate the wallet.
However, I was not happy with this approach because this way some entropy is lost.
Also, I didn't want to just hash the rolls because that's one way conversion.
Instead, the idea is to just get a big enough base6 number, convert it to a base16 number and that's it.
No crypto wizardry but pure pyhsical randomness, actual dice rolls **are** the seed.

The base6 number "has" to be exactly 98-digits, and the first digit can be either 0 or 1. This is achieved by performing modulo 2 on the first roll only, so the even roll will result in 1 and odd in 0. The biggest number you can represent like this is:

`0x0D5FC08FC370813C337211B2A487C6B76111CA0BFFFFFFFFFFFFFFFFFFFFFFFF`

which is:

`15555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555`

in base6, equivalent to rolling:

`26666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666`

the l is:

`0x1000000000000000000000000000000014DEF9DEA2F79CD65812631A5CF5D3ED`

and already, any seed generated is divided by the l and remainder used as the private key, so any number bigger than l is a waste of rolls. The above number (`155...`) is about `0.835*l`, so we're almost using the entire domain of possible seeds, mapped 1-to-1 to your dice rolls!

## Printable Version Notes

This version will show QR codes for both address and privte keys. In addition, it should be nicely foldable when printed.
