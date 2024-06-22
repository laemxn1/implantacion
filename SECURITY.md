# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## Reporting a Vulnerability


In chat2.php reflected XSS is possible.
This because chatdisplay.php returns unsanitized or unencoded user input.
The project is not maintained, but there are people who use this.

Please update the code:
Original code 
```
<script>
    function displaychat() 
    {
    
        var xmlhttp = new XMLHttpRequest();
        xmlhttp.onreadystatechange = function() 
        {
            if (this.readyState == 4 && this.status == 200)
            {
                document.getElementById("chats").innerHTML = this.responseText;
            }
        }
        xmlhttp.open("GET", "chatdisplay.php", true);
        xmlhttp.send();
    }
   setInterval(displaychat,100);
</script>
```

Could be 
```
<script>
    function displaychat() 
    {
        var xmlhttp = new XMLHttpRequest();
        xmlhttp.onreadystatechange = function() 
        {
            if (this.readyState == 4 && this.status == 200)
            {
                document.getElementById("chats").textContent = this.responseText;
            }
        }
        xmlhttp.open("GET", "chatdisplay.php", true);
        xmlhttp.send();
    }
    setInterval(displaychat, 100);
</script>

<div id="chats"></div>

```
By using textContent, any HTML or JavaScript in the response will be displayed as text rather than executed. However, ensure that the server-side code sanitizes and validates user input to prevent any XSS attack vectors.


