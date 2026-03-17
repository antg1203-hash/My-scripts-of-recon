# My-scripts-of-recon
just experimenting and doing recon


curl -s https://www.google.com/robots.txt | grep "Disallow" > google.txt

grep -i "api\|debug\|internal\|admin\|backup\|config\|env\|db" tesla_total.txt | head -n 30

ls -lh tesla_total.txt

timeout 60s waybackurls tesla.com > tesla_total.txt

ssh bandit0@bandit.labs.overthewire.org -p 2220

"HOW TO TRY TO TRICK CLOUDFLARE WITH CURL (NOT GUARANTEED)"
curl -s -L -A "Mozilla/5.0 ..." https://www.carsdirect.com/robots.txt | grep -i disallow

curl -s -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36" https://www.carsdirect.com/robots.txt | grep -i disallow

