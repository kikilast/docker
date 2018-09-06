#Docker MongoDB

mongodb in docker with account/password

##1

建立mongo的docker container
```cmd
docker run -d --name some-mongo -p 27017:27017 -v /dataMongo:/data/db mongo
```

進到容器裡面
```cmd
docker exec -it some-mongo /bin/bash
```

進到mongodb
```cmd
mongo
```

建立Database
```cmd
use test

建立該DB的使用者
```cmd
db.createUser({
	user:'root',
	pwd:'1234',
	roles:[{role:'readWrite',db:'test'}]})
```

離開mongo
```cmd
exit
```

進入容器
```cmd
docker exec -it some-mongo /bin/bash
```

進Mongo
```cmd
mongo 127.0.0.1:27017/test -u root -p 1234
```