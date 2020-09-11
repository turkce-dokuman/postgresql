# PostgreSQL sunucusunda şema, veritabanı, tablo vs. oluşturabilmek için CREATE kullanırız.
### Başlıklar
* [Veritabanı Oluşturmak](#create-database)
* [Tablo Oluşturmak](#create-table)

#### CREATE DATABASE 
``CREATE DATABASE``, postgreSQL sunucusunda bir veritabanı oluştrur. Varsayılan olarak komutu yürüten kullanıcı veritabanı sahibi olur eğer yetkisi yoksa onu oluşturamaz. 
Örnek:
```SQL 
    CREATE DATABASE postgresql_dersleri;
```
##### Seçenekler 
* [OWNER](#owner)
* [ENCODING](#encoding)
* [CONNECTION LIMIT](#connection-limit)
#### OWNER
Bir kullanıcı için veritabanı oluşturmak için `OWNER` seçeneği eklenir ve kullanıcı adı yazılır.

Örnek:
```SQL 
    CREATE DATABASE postgresql_dersleri 
    WITH 
    OWNER = ahmet;
```

#### ENCODING
Veritabanı oluştururken karakter seti seçilir bu seçeneği kullanmadığınızda `postgresql` kendi otomatik seçer. Desteklenen karakter setleri [bknz](https://www.postgresql.org/docs/10/multibyte.html)
Örnek:
```SQL 
    CREATE DATABASE postgresql_dersleri 
    WITH 
    OWNER = ahmet 
    ENCODING = 'UTF8';
```
#### CONNECTION LIMIT
PostgreSQL veritabanı bağlantı sınırı varsayılan olarak bu -1'dir sınırı yoktur seçenekleri kullanarak bunu değiştirebilirsiniz.
```SQL 
    CREATE DATABASE postgresql_dersleri 
    WITH 
    OWNER = ahmet 
    ENCODING = 'UTF8'
    CONNECTION LIMIT = 10;
```
##### [BKNZ](https://www.postgresql.org/docs/9.1/app-createdb.html)
#### CREATE TABLE 
Veritabanında tablo oluşturur. Tablonun sahibi komutu çalıştıran kullanıcıya ait olacaktır. 
###### [Veri Tipleri](https://www.postgresql.org/docs/9.5/datatype.html)

```SQL 
    CREATE TABLE posts(
	id serial not null primary key, -- serial : otomatik artan değer. not null : boş olamaz. primary key : birincil anahtar. 
	title varchar(80) not null, -- varchar : limitli veri tipi (80)
	content text not null, -- text : limitsiz uzunluğa sahip.
	posted_by varchar(50)
)
```

