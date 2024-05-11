# Proxmark3

Welcome to my Proxmark3 repository! Here, I delve into the realm of cloning access cards using the Proxmark3 Easy equipped with Iceman firmware. If you're curious about this device and how to wield its powers, you can find all the details in their official documentation.

### Disclaimer
_Please note that the contents of this repository are for educational and experimental purposes only. Any usage of the information or tools provided here for unauthorized access or malicious activities is strictly prohibited and may be illegal. I do not endorse or condone any illegal or unethical use of the techniques or technologies discussed within this repository. Users are solely responsible for their actions and should ensure compliance with applicable laws and regulations in their jurisdiction._

## Cloning

In this particular scenario, I'm essentially updating an outdated card with expired credentials to reflect the new credentials from a replacement card.

Let's start by examining the new card to determine its specifications. Since I'm aware that it operates on a 125kHz frequency, I'll position it on the LF antenna and initiate the lf search command to gather more information. If there's any uncertainty, the auto command can be used as an alternative to automatically detect the card type.
