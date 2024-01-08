# lazy-ctfs
A lot of lazy machines lately. This isn't for every box, this is just to rate how lazy the box is.

To check if a machine is lazy:
1. Set your target
   ```bash
   export target=127.0.0.1
   ```

2. Run nmap against 80/443 for quick DNS records. Add results to /etc/hosts
   ```bash
   nmap -sV -sC -p 80,443 $target | tee /tmp/nmap_output.txt; echo "Try adding these to your /etc/hosts file"; grep "DNS:" /tmp/nmap_output.txt | sed 's/.*DNS:\(.*\)/\1/' | tr ',' '\n' | sed 's/^[ \t]*//' | tee /tmp/dns_records.txt
   ```

3. Add the original/initial target to the dns_records.txt
   ```bash
   echo $target >> /tmp/dns_records.txt
   ```

4. Run nuclei against the target.
   ```bash
   ~/go/bin/nuclei -l /tmp/dns_records.txt -fhr -uc -headless -as -silent
   ```
