# Hacking server fan speed control : 



I use a second-hand racked server with a hardware RAID card to host a family file cloud system  plus some few custom web frontpages to access cave's hardware from the outside world. (Owncloud v10, Ubuntu OS on a 250 RAID 0 with 2drives, and Data stored on a 2To RAID 5 with 5 drives plus one automatic hotswap spare)



<img src="server.png" alt="IMG_20190223_163526" style="max-width:70%;" />

The server has high quality lights-out ethernet management and good specs, and is available at very low prices because it has been in use in server houses for 10 years already. It is both convenient to access such professional hardware, and ecologically interesting to continue using still functionnaly capable machines that have been disposed because their performances are not up to modern standard in large server data storage houses.



The issue with this, is that in data centers, the noise isn't an issue. In fact, server fans are "consumable" and are used at speeds that exeeds the real cooling needs, to prevent any failures. For the low computing power use that we make 

from this server at home, we don't need such heavy fans. But unfortunately, the fan speed in relation to temperature is controlled by the motherboard and isn't parametrable from the network management port interface.

On the other hand,  turning the server off if one fan breaks and stops turning is a handy security feature.

So, to keep the best and improve the issues, i used an arduino as a "man in the middle", between fans and motherboard.

The fans uses open collector outputs to generate a PWM signal depending on the rotation speed, while another PWM sinal is sent by the motherboard.

With an osciliscope, i read the correspundancy between the command pwn and the resulting pwn that fans sent when executing the commands.

I used this as a conversion function, and make the arduino able to send a command to the fan with a decreasing factor depending on user input, while maintaining a "fake answer" to the motherboard, to keep the built-in fan security system in a peacefull state.

With the reading of the actual answer of the fans by the arduino, i can also detect if the signal turns to a complete stop, in case of a fatal failure on one fan for example, and in such a condition, update the fake answer to the motherboard to a flat signal, to trigger the soft power off of the server via the built-in fan speed security system.