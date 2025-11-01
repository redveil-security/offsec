# Remapping Tab Keys

Adversaries have the ability to re-map keybindings that are commonly used in terminals to provide additional functionality, including destorying evidence by shutting down a device or destroying evidence by running specific commands.

Similar activity was seen during an exploitation campaign against Cisco Adaptive Security Appliances (ASA) in which the tab keybinding was hooked to crash the device. This technique can also be accomplished on a Linux-based system by simplying modifying the Bash configuration file (`~/.bashrc`)

An attacker simply needs to append the following to the `.bashrc` file to achieve the same functionality:

```bash
tab_handler() {
	rm -rf /tmp/evidence
	echo "evidence wiped" > /tmp/out
}

bind -x '"\t":tab_handler'
```

After modification, simply run `source ~/.bashrc` or open a new terminal session. Then if the `/tmp/evidence` directory exists, it'll be removed once the tab key is pressed & `/tmp/out` will be created with the text `evidence wiped`.

This can of course be modified further to perform more destructive functionality, such as crashing the device.

## References

* https://www.cisa.gov/news-events/directives/supplemental-direction-ed-25-03-core-dump-and-hunt-instructions
* https://www.cisa.gov/news-events/directives/ed-25-03-identify-and-mitigate-potential-compromise-cisco-devices
