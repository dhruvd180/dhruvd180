## Welcome to D180's site!

I am a web developer, Scratch coder, and Python enthusiast who makes websites, and functional projects for fun but doest really use github, I mainly use Repl.it, and I'm looking for help hosting Python REPLS and connecting to cloud servers for Scratch and Turbowarp.

My main issue with my Cloud_Connector file is that on REPL.it, repls shutdown and go to sleep after about an hour. 
I believe you can use Flask to solve the issue but I have not been successful so far, please fork this repo with your code and ideas if you can solve this issue.
### Markdown

Here is my code for the Cloud_Connector
Username and password are CENSORED, as well as the PROJECTID(XXXXXXXXXX).
Weather code from a web tutorial.
Encoder by TheCloudDev on scratch.

```markdown
from bs4 import BeautifulSoup
import requests
from scratchclient import ScratchSession

session = ScratchSession("MYUSERNAME", "MYPASSWORD")
headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3'}

def weather(city):
    city=city.replace(" ","+")
    res = requests.get(f'https://www.google.com/search?q={city}&oq=weather&aqs=chrome.0.35i39l2j0l4j46j69i60.6128j1j7&sourceid=chrome&ie=UTF-8',headers=headers)
    print("Searching......\n")
    soup = BeautifulSoup(res.text,'html.parser')   
    location = soup.select('#wob_loc')[0].getText().strip()  
    time = soup.select('#wob_dts')[0].getText().strip()       
    info = soup.select('#wob_dc')[0].getText().strip() 
    weather = soup.select('#wob_tm')[0].getText().strip()
    print(location)
    print(time)
    print(info)
    print(weather+"°C") 
global chars
chars = "abcdefghijklmnopqrstuvwxyz0123456789+-. _"
def encode(text):
    global chars
    text = text.lower()
    encoded = ""
    length = int(len(text))
    for i in range(0,length):
        try:
            x = int(chars.index(text[i])+int(9))
            encoded = encoded + str(x)
        except ValueError:
            print("!")
    return encoded
def decode(text):
    decoded = ""
    y = 0
    for i in range(0,len(text)//2):
        x = chars[int(str(text[y])+str(text[int(y)+1]))-9]
        decoded = str(decoded)+str(x)
        y += 2
    return decoded
def get_query():
  connection = session.create_cloud_connection(XXXXXXXXXX)
  query=(connection.get_cloud_variable("query"))
  query=decode(query)
  tbe = weather(query)
  tbe = encode(tbe)
  connection.set_cloud_variable("in_query", tbe)
x = 1
while x > 0:
  get_query()
```

