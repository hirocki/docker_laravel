
# Docker_laravel 開発環境構築用
+-------------------------------+
|                               |
|　Last update 2019/08/05       |
|       Docker_laravel          |
|                               |
+-------------------------------+

- 環境ビルド
```
docker-compose build && docker-compose up -d
```
- Laravelインストール
```
winpty docker exec -it Laravel bash
```
```
laravel new
```
```
composer update
```
```
mv .env.example .env
```
- .env書き換え
```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db
DB_USERNAME=user
DB_PASSWORD=pass
```
- キー生成
```
php artisan key:generate
```

もし、[ReflectionException]とかClass ‘HogeHoge’ not foundのようなエラーが出たら、次のコマンドでオートロードの定義を更新
```
php artisan db:seed
```
- 完成
```
curl http://localhost:8080  
```


## Mysqlコマンド
```
$ winpty docker exec -it コンテナID bash

mysql -u root -p

show databases;

use データベース名;

show tables;
```



## 初期化コマンド
### git
```
git checkout .  
git clean -df  
```

### docker
```
docker stop $(docker ps -q)  
docker rm $(docker ps -q -a)  
```
