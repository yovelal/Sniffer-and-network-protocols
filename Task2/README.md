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

# Server - In each transmission of d packets:
1. If only one package is missing from the d packages, then the server knows how to recover it by doing XOR of all the packets that came and with e. for example: if d=3 and packet2 is missing then: e = m1 XOR m2 XOR m3 . The server has m1, m3 and e and can therefore calculate m2 by: m2 = e XOR m1 XOR m3 <br />
2. If more than one packet is missing, the server notifies the client that a retransmission is needed .<br />
3. If the server received all d packets then check if server_e = client_e . if not the server ask for retransmission , else the server send to the client a FIN message.<br />

# Defenses against attack:
we would like a mechanism to identify an attacker that will work during the entire connection. In each transmission of d packets the server will check :<br />
1. If at least 80% of the messages (0.8*d) didn’t arrive at least 2 times .<br />
2. If a specific packet does not arrive at least 5 times.<br />
3. If all d packets were retransmitted at least max(8,0.5*d) times.<br />
<br />If one of the conditions is met, the server sends the client a warning message about a high probability of an attack. The client will close the connection.<br />
In addition, assume the attacker tries to prevent the connection by dropping the handshake packet (which contains e and d). Our protocol makes the attack more difficult by having the number d be randomly rechosen, so the packet of the handshake is dynamic.
