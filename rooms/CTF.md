# [CTF collection Vol.2](https://tryhackme.com/room/ctfcollectionvol2)

## Easter egg

1. Easter 1  
Ran nmap scan and noticed there was a http-robots.txt:  
went to robots.txt and there were numbers: 
45 61 73 74 65 72 20 31 3a 20 54 48 4d 7b 34 75 37 30 62 30 37 5f 72 30 6c 6c 5f 30 75 37 7d  
Paste this in cyber chef and covert from hex

<details>
  <summary><strong>Answer</strong></summary>
 
 **THM{4u70b07_r0ll_0u7}** 

</details>

2. Easter 2

<details>
  <summary><strong>Answer</strong></summary>
 
 **s** 

</details>

3. Easter 3  
performed a dirb on the target and saw /login  
Inspect the HTML content 

<details>
  <summary><strong>Answer</strong></summary>
 
 **THM{y0u_c4n'7_533_m3}** 

</details>


4. Easter 4


5. Easter 5


6. Easter 6


7. Easter 7


8. Easter 8


9. Easter 9


10. Easter 10


11. Easter 11


12. Easter 12


13. Easter 13


14. Easter 14


15. Easter 15


16. Easter 16  


<br>
go to the [target ip]/game2/  
Run the below JavaScript in the console to click all buttons

```javascript
// 1. Create one empty data object
const combinedData = new URLSearchParams();

// 2. Grab every hidden input from ALL forms and add them to our object
document.querySelectorAll('input[type="hidden"]').forEach(input => {
    combinedData.append(input.name, input.value);
});

// 3. Add the "submit" button value manually (since it's common to all 3)
combinedData.append('submit', 'submit');

// 4. Send EVERYTHING at once in one single POST
fetch(window.location.href, {
    method: 'POST',
    body: combinedData,
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
    }
}).then(response => response.text())
  .then(html => {
      // This replaces your current page with the server's response
      document.open();
      document.write(html);
      document.close();
  });

```

<details>
  <summary><strong>Answer</strong></summary>
 
 **THM{73mp3r_7h3_h7ml}** 

</details>

17. Easter 17
18. Easter 18
19. Easter 19

Performed a dirb on the target machine and found /small
[Target Machine]/small

<details>
  <summary><strong>Answer</strong></summary>
 
 **THM{700_5m4ll_3yy}** 

</details>




20. Easter 20

