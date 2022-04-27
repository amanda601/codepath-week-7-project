
<h1> Wordpress Pentesting </h1>

<h3> Time Spent: maybe like 7 hours </h3>

<h3> 1. Stored XSS </h3>
<p>Discovered by Jouko Pynnönen of Klikki Oy <a href=url>https://klikki.fi/wordpress-stream-plugin-stored-xss-remote-code-execution/</a>
      
 To begin this exploit, I wrote a command in order to overflow the mySQL system in order to push through the script.

I needed aproximatly 64 kilobytes worth of charachters to activate the exploit due to mySQL having a charachter limit of 64kbs.
 


cout<<"A"<<*<<65600;
(I used this to make a ton of character data to make it easier)

Once I had the data ready, I wrote my exploit.

<a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px ’></a>

Once I loaded up all of the letter data, I was in.     
     
      
  ![XSS](https://user-images.githubusercontent.com/98411280/164501649-2c82caa8-e81b-4502-bb1c-39e458714a00.gif)

<h3> 2. Brute Force Login with WPScan and wordlist </h3>
      
<p>WPScan can ennumerate users and generate passwords if you use a wordlist.
  -use command: wpscan --url wpdistillery.vm -passwords passwords.txt
          
          

   
   
   ![password](https://user-images.githubusercontent.com/98411280/164503512-0689566e-425f-4a5b-a3b6-c4fa511929f5.gif)

   On the left, the admin tab is open with a list of users; on the right, the output of the preceding command is printed, exposing the user's passwords.
   Using the wpscan results, I am able to log in as the user Franz.
   
   
   
   
   
<h3>3. Another Stored XSS </h3>

An author or contributor level account is required for the following XSS attack due to needint to escalate privalges.

This one took me a little longer to figure out the code. When trying to write the code out, GitHub kept thinking it was a link and I couldn't get it to format correctly. See gif below for code used.


This code could easily be made more malicious by using a style tag to cover the entire page coupled with the onmouseover executioner.

![linkXSS](https://user-images.githubusercontent.com/98411280/164507186-eac16c8f-45b9-4249-acdb-e2f5839fa830.gif)


Wordpress will then proccess the following code and create this link:
      
 ![ezgif-4-9288074b93](https://user-images.githubusercontent.com/98411280/164507767-719cc9d1-1e93-4401-a16c-ebad9057f645.gif)
