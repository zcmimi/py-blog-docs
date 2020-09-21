提供了过滤器`encrypt`

`text|encrypt(password)`将`text`用密钥`password`加密(`aes-128-ecb-pkcs7`)

并提供了前端`javascript`解密函数`de(data,password)`

使用示例:

```html
<div id="md-body" class="md-body" hidden>{{md(content)|encrypt(password)}}</div>
<div class="mdui-textfield mdui-textfield-floating-label">
    <label class="mdui-textfield-label">请输入密码:</label>
    <input class="mdui-textfield-input" type="password" id="passwd">
</div>
<script src='https://cdn.jsdelivr.net/gh/brix/crypto-js@4.0.0/crypto-js.min.js'></script>
<script>
    function de(data,passwd){
        while(passwd.length%16)passwd+='\0';
        var decrypt=CryptoJS.AES.decrypt(
            data,
            CryptoJS.enc.Utf8.parse(passwd),
            {
                mode: CryptoJS.mode.ECB,
                padding: CryptoJS.pad.Pkcs7
            }
        );
        return decrypt.toString(CryptoJS.enc.Utf8);
    }
    var md_body=document.getElementById('md-body'),
        passwd=document.getElementById('passwd');
    const content=md_body.innerText;
    passwd.oninput=function(){
        var data=de(content,this.value);
        if(data){
            md_body.innerHTML=data;
            this.parentElement.hidden=1;
            md_body.hidden=0;
            highlight(),gentoc("md-body"),katex_();
        }
    }
</script>
```