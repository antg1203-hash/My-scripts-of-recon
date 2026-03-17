# My-scripts-of-recon
just experimenting and doing recon


curl -s https://www.google.com/robots.txt | grep "Disallow" > google.txt

grep -i "api\|debug\|internal\|admin\|backup\|config\|env\|db" tesla_total.txt | head -n 30

ls -lh tesla_total.txt

timeout 60s waybackurls tesla.com > tesla_total.txt

ssh bandit0@bandit.labs.overthewire.org -p 2220