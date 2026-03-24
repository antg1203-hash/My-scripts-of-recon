# My-scripts-of-recon and tinkering
just experimenting and doing recon on my phone with termux.

"BASIC RECON"
curl -s https://www.google.com/robots.txt | grep "Disallow" > google.txt

grep -i "api\|debug\|internal\|admin\|backup\|config\|env\|db" tesla_total.txt | head -n 30

ls -lh tesla_total.txt

timeout 60s waybackurls tesla.com > tesla_total.txt

ssh bandit0@bandit.labs.overthewire.org -p 2220

"NETWORK RECON (NO NEED OF ROOT, AT MOST JUST PROOT)"

nmap localhost (you can use --unprivileged)

nmap (example IP)/24

"THE PLACES I USUALLY USE ON TERMUX"
proot-distro login debian
or
proot-distro login Ubuntu 

"HOW TO TRY TO TRICK CLOUDFLARE WITH CURL (NOT GUARANTEED)"
"USER-AGENT"
curl -s -L -A "Mozilla/5.0 ..." https://www.carsdirect.com/robots.txt | grep -i disallow

curl -s -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36" https://www.carsdirect.com/robots.txt | grep -i disallow

from fake_useragent import UserAgent
ua = UserAgent()
headers = {'User-Agent': ua.random}
response = requests.get(url, headers=headers)

# pip3 install seleniumbase
from seleniumbase import Driver

# initialize driver with UC mode enabled
driver = Driver(uc=True)

# set target URL
url = "https://www.scrapingcourse.com/cloudflare-challenge"

# open URL using UC mode with a 4-second
driver.uc_open_with_reconnect(url, reconnect_time=4)

driver.sleep(10)

# attempt to click the CAPTCHA checkbox
driver.uc_gui_click_captcha()

# wait for CAPTCHA solving
driver.sleep(10)

# ... scraping logic

# close the browser and end the session
driver.quit()


