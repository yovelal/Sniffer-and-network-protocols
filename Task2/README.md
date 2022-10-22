# Adversary:
Our attacker can insert a list of inputs that packets containing them will be dropped. Since our protocol can handle the dropping of one packet, the attacker will drop at least 2 packets.<br />
Implementation:<br />
• In order for the attacker to be able to listen to the port and print the packets, we used scapy.<br />
• In order for the attacker to be able to drop packages, we used iptables commands.<br />

# Client:
In this task, before sending the messages containing the text, the following steps were performed :<br />
1. The client will choose a random number d which will be the number of messages the client will send.<br />
2. The client will compile a list of messages to send and calculate e in the following way: e = m1 XOR m2 XOR m3 … XOR md<br />
3. The client will send the server a message containing e and d. If the client does not receive a confirmation message about the handshake from the server, it will return to the first section.<br />
4. The client will send the d messages to the server.<br />
5. The client will wait for a message from the server, if the message is :<br />
- FIN : The client will close the connection.<br />
- Retransmission: The client will send the d messages again.<br />
