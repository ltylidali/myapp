# myapp
This is I write an implementation of the HTML element operation simple js, realized the ajax POST and GET data transmission, as well as a Map collections.
Use examples
<!DOCTYPE html>
<html>
<head>
    <title>Client</title>
    <script src="/static/myapp.js"></script>
    <script type="text/javascript">
        var my = new myapp();
        window.onload=function(){
            var button = my.get('#sub');
            button.on('click',function(){
                var username = my.get('#username');
                var password = my.get('#password');
                var key = my.get('#key');
                if(username.value() == ''){
                    alert('Please enter the username');
                    return false;
                }
                if(password.value() == ''){
                    alert('Please enter the password');
                    return false;
                }
                my.ajax({
                    type:'POST',
                    url:'/login',
                    data:'username='+username.value()+'&password='+password.value()+'&key='+key.value(),
                    success:function(data){
                        data = eval('('+data+')');
                        if(data.success){
                            my.get('#msg').html(data.msg);
                        }else{
                            alert('Login failed!');
                            my.get('#msg').html(data.msg);
                        }
                    }
                });
            });
        }
    </script>
</head>
<body>
  <form id="loginform" method="POST">
    <table id="logintable">
        <tr>
          <td>userName:</td>
          <td><input type="text" name="username" id="username" /></td>
        </tr>
        <tr>
          <td>passWord:</td>
          <td><input type="text" name="password" id="password" /></td>
        </tr>
        <tr>
          <td colspan="2"><input type="button" id="sub" value="test ajax"/>
        </tr>
      </table>
      <div id="msg"></div>
  </form>
</body>
</html>          
