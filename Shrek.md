# Shrek Machine 

__________________________________________________________________________________________________________________________________________________________________________________
DISCLAIMER 

****I assume you already know how to do a scan of ports and services, this writing is intended to help those who have trouble getting root shell, it will not tell the location of the flags, it is your challenge to do so, good luck.

-𝓣𝓸𝓻𝓸𝓹𝓸𝓿 𓅓****
__________________________________________________________________________________________________________________________________________________________________________________

When we search through the machine service http, we find that the robots directory contains interesting data...
![image](https://user-images.githubusercontent.com/73258250/144330782-28e1896f-b680-4c73-bbbd-9d76e7f1ff3f.png)

That secret file contains id_rsa credentials, so maybe we got ssh acces, but, which user?
![image](https://user-images.githubusercontent.com/73258250/144330898-abab11f4-4be1-42db-8377-5822d8e08d53.png)

we got to grant permissions to the file, so we do:
            
            chmod 600 id_rsa
then we can use it to get a ssh sesion.
![image](https://user-images.githubusercontent.com/73258250/144331208-dd729765-37e4-46f2-8ceb-eef1458a007e.png)
we are inside! now, we check the machine db making:
  
    mysql -u root -p
the password is "password", we found by trying default passwords.

![image](https://user-images.githubusercontent.com/73258250/144331630-57afeb54-39d3-4488-a780-5aaf10d3a077.png)

we find ftp credentials, so we check ftp and get...

![image](https://user-images.githubusercontent.com/73258250/144331794-4e67ca61-0f4b-4b17-bfae-8b0fb0e5987b.png)

There is another interesting file, if we get and then read it we can get the donkey´s password

![image](https://user-images.githubusercontent.com/73258250/144331932-f686f5f5-3eec-4e42-bfbc-31e603da08e5.png)

We have a donkey´s access, and listing sudo permissions we get that tar is running with sudo...

    sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh

![image](https://user-images.githubusercontent.com/73258250/144332321-22c3d443-cf66-4a2a-a3ae-858ff8424b65.png)

Exploiting this give us a root shell! finally! :)

![image](https://user-images.githubusercontent.com/73258250/144332402-4646cb76-3af3-4b2f-ab78-8fa8fab9acda.png)
_______________________________________________________________________________________________________________________________________________________________________________
## Getting a root shell with shrek´s account

as Shrek, we can use gdb, and it is precompiled with python, so we can exploit it by using this command:

    gdb -nx -ex 'python import os; os.execl("/bin/sh", "sh", "-p")' -ex quit

![image](https://user-images.githubusercontent.com/73258250/144332102-a4de759b-6568-4a0c-88d8-3b69407566b4.png)


If you get stuck or have doubts, you can contact me via Discord: 
**𓅓【𝓣𝓸𝓻𝓸𝓹𝓸𝓿】𓅓#6473

Nice KoTH, fairplay forever
_______________________________________________________________________________________________________________________________________________________________________________
