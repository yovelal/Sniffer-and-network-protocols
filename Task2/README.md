# Adversary:
Our attacker can insert a list of inputs that packets containing them will be dropped. Since our protocol can handle the dropping of one packet, the attacker will drop at least 2 packets.<br />
Implementation:<br />
• In order for the attacker to be able to listen to the port and print the packets, we used scapy.<br />
• In order for the attacker to be able to drop packages, we used iptables commands.<br />
