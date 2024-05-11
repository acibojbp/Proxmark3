# Proxmark3

Welcome to my Proxmark3 repository! Here, I delve into the realm of cloning access cards using the Proxmark3 Easy equipped with Iceman firmware. If you're curious about this device and how to wield its powers, you can find all the details in their [official documentation](https://github.com/RfidResearchGroup/proxmark3).

![Screenshot 2024-05-11 043752](https://github.com/acibojbp/Proxmark3/assets/164168280/353803c0-0ee4-481d-a09d-5449438d6516)

### Disclaimer
_Please note that the contents of this repository are for educational and experimental purposes only. Any usage of the information or tools provided here for unauthorized access or malicious activities is strictly prohibited and may be illegal. I do not endorse or condone any illegal or unethical use of the techniques or technologies discussed within this repository. Users are solely responsible for their actions and should ensure compliance with applicable laws and regulations in their jurisdiction._

## Updating 125kHz Access Cards

In this particular scenario, I'm essentially updating an outdated card with expired credentials to reflect the new credentials from a replacement card.

Let's start by examining the new card to determine its specifications. Since I'm aware that it operates on a 125kHz frequency, I'll position it on the LF antenna and initiate the `lf search` command to gather more information. If there's any uncertainty, the `auto` command can be used as an alternative to automatically detect the card type.

![Screenshot 2024-05-11 043946](https://github.com/acibojbp/Proxmark3/assets/164168280/a5096c98-5768-4162-8546-c5646467b344)

It appears that we've detected a **valid EM410x ID**. These IDs can be written to cards equipped with **T55xx chips**. We can view the EM410x ID here, and to confirm it further, we can utilize the `lf em 410x reader` command.

![Screenshot 2024-05-11 044009](https://github.com/acibojbp/Proxmark3/assets/164168280/13ac5469-4bd2-4874-a76f-f819390718b9)

We can perform the same process on the outdated card and observe that it still holds the old credentials.

![Screenshot 2024-05-11 044139](https://github.com/acibojbp/Proxmark3/assets/164168280/51de5b87-0f92-4ba4-bc8c-639654d3357b)

I'm about to clone the new ID onto the old card, effectively updating it with the new credentials. I'll execute the `lf em 410x clone --id [ID]` command for this purpose. To ensure the cloning process was successful, I'll then use the `lf em 410x reader` command to verify.

![Screenshot 2024-05-11 044224](https://github.com/acibojbp/Proxmark3/assets/164168280/915d3003-56ec-4380-9726-316bb1f7e3da)

However, it's apparent that the card still retains the old ID. Why could this be happening? One approach we can take is to attempt to wipe the card before writing to it using the command `lf t5 wipe`, followed by verifying its status with `lf t5 detect`.

![Screenshot 2024-05-11 044352](https://github.com/acibojbp/Proxmark3/assets/164168280/8f8f5a7d-8867-4cab-b754-24875dd33026)

An error message appears: **"Could not detect modulation automatically. Try setting it manually with `lf t55xx config`."**

This suggests that the card might have been previously written on using a cheap China cloning device (the blue ones with two buttons, read/write), which tends to automatically set passwords on the cards whenever they are written to, for some reason.

Let's proceed to see if we can crack the password using the command `lf t5 chk`.

![Screenshot 2024-05-11 044312](https://github.com/acibojbp/Proxmark3/assets/164168280/5ab9f31f-4207-4eae-90d7-181a4d3ce4cc)

This confirms that the card is indeed password protected, and we've successfully discovered a valid password!

Now, we'll attempt to wipe the card once more, but this time we'll include the password. We can do this by executing the command `lf t5 wipe -p [password]`. Afterward, we'll use the command `lf t5 detect` to ensure that the wiping process was successful.

We can also verify this by executing the command `lf search` again. We should expect to see the line **"No known 125/134 kHz tags found!"** to confirm that the card has been successfully wiped.

![Screenshot 2024-05-11 044455](https://github.com/acibojbp/Proxmark3/assets/164168280/1ab89ea1-e7f2-46e5-a876-da4aa3e8cb59)

From this point, we can proceed by executing the cloning command once more: `lf em 410x clone --id [ID]`, and then confirming the cloning process using `lf em 410x reader`.

![Screenshot 2024-05-11 044539](https://github.com/acibojbp/Proxmark3/assets/164168280/f4ad6da3-366a-4d2a-bf6a-e4de4d137963)

We now observe that the cloning process was successful.

In conclusion, through a series of steps, we successfully updated an outdated access card with new credentials using the Proxmark3 device. Despite encountering challenges such as password protection, we navigated through them effectively by cracking the password and ensuring a thorough wiping process. Ultimately, we accomplished our goal of cloning the new ID onto the old card, thus enabling seamless access with updated credentials.







