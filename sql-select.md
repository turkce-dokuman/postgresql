# Bir veya birden fazla tablodan satırları çeker.

### Başlıklar
* [SELECT](#select)
* [FROM](#from)
* [WHERE](#where)
* [AS](#as)
* [LIKE](#like)
* [ORDER BY](#order-by)
* [OR](#OR)
* [AND](#and)
* [NOT IN](#not-in)
* [DISTINCT](#distinct)
* [LIMIT](#limit)
* [OFFSET](#offset)
#### SELECT
Bir tabloda tüm(*) veya belirli [kolon_1, kolon_2,...] kolonları çekmek için seçim yapmanıza olanak tanır.

```SQL
    SELECT [*] | [kolon_1, kolon_2,...]
```
### FROM 
Seçtiğiniz kolonları vs hangi tablodan çekeceğinizi seçmenize olanak tanır.
```SQL 
   SELECT * FROM tablo_adi;

```
`SELECT *` kullanıldığında belirtilen tablodaki bütün sütünları çekecektir. Bu da sorgu süresini biraz daha uzatıyor.

Tablodaki bütün kayıtları getirir.

#### WHERE
Seçtiğiniz kayıtların hepsini istemeyebilirsiniz `WHERE` komutu belirlediğiniz koşulu karşılayan kayıtların dönmesi için kullanılabilir

```SQL
    SELECT isim, eposta, telefon_numarasi, yas FROM kullanicilar WHERE yas = 21
```
Bu sorguda yaşı 21 olan kullanıcıların verilerini döndürür. Tabikide sadece eşit(=) operatörüyle sınırlı değildir. 
```SQL
    -- > : Büyüktür operatörü 
        WHERE yas > 21 
           -- yaşı 21'den büyük olan kullanıcıların verilerini getirir.
    -- < : Küçüktür operatörü
            WHERE yas < 21 
           -- yaşı 21'den küçük olan kullanıcıların verilerini getirir.
    -- <>: Küçüktür ve büyüktür bir arada kullanıldığında eşit olmayan yani 
            WHERE yas <> 21 
            -- yaşı 21'e eşit olan kullanıcıların verisini getirmez. != bu operatör ile aynı işlevi yapar.
    -- <= : Küçük veya eşit bunu ayni diyelimki biz yaşı 21'e eşit ve ondan küçük olanları çekmek istiyoruz bu kullanım yeterli
```
#### AS
`AS` komutu takma ad için kullanılabilir. Bu ne demek oluyor ?
Şöyle, diyelimki bizim `isim` diye bir kolunumuz var ama bunu `ad` diye kullanmak istiyorum
```SQL
    SELECT isim AS ad FROM kullanicilar WHERE yas > 21
```

#### LIKE 
`LIKE`, kolonlar üzerinde arama yapmamıza olanak sağlıyor. Kullanıma geçelim.
> `%dizge%`,`dizge%`,`%dizge`
```SQL
    SELECT * 
    FROM kullanicilar 
    WHERE isim -- burda hangi kolon üzerinden arama yapmak istiyorsanız onu belirtin.
    LIKE 'ahmet'
```
Burada `ismi`, `ahmet` ile eşleşen tüm satırları döndürecek. Bu şekilde çok işlevsel değil `WHERE isim='ahmet'` ile aynı işlevi yapar. Fakat daha farklı kullanımları var. 
``WHERE 'isim' LIKE 'a%'`` burda `isim` sütünunda `'a'` ile başlayan tüm kayıtlar gelecek. Yani anlamı şu 1. karakteri `'a'` ondan sonraki karakterlere bakmaz.

``WHERE 'isim' LIKE '%met'`` burdada `isim` sütünunda `'met'` ile biten tüm kayıtlar gelecek. Yani anlamı şu sondan 3 karakteri `'met'` ile eşleşen tüm kayıtlar demek. [Daha Fazlasına Burdan Bakınız](https://www.postgresql.org/docs/current/functions-matching.html)

#### ORDER BY
`ORDER BY`, sonuçları belirtilen kolona göre listelememizi sağlıyor. Yani sorgu çekerken normal durumlarda id'ye göre getiriyor.
>``ASC``, ``DESC``
```SQL 
    SELECT * FROM kullanicilar ORDER BY yas 
```
Bu durumda yaşı küçükten büyüğe doğru sıralar. Büyükten küçüğe doğru sıralamak için ``DESC`` kullanılır.
```SQL 
    SELECT * FROM kullanicilar ORDER BY yas DESC 
```
Bu kez tersten listeleyecek tabi bu rakamlarla sınırlı değil alfabetik sıralamada yapar normal durumda A'dan, Z'ye sıralar.

#### AND 
`AND`, sorguya yeni bir koşul eklemek için kullanılır.
```SQL
    SELECT * FROM kullanicilar WHERE yas > 21 AND yas > 16
```
#### OR 
`OR`, sorguda 1. koşul karşılanmazsa bir sonraki koşul için kullanılır. 
```SQL
    SELECT * FROM kullanicilar WHERE yas > 21 OR yas > 16
```
#### NOT IN
`NOT IN`, içinde olmayan sorguları getirir.
```SQL
    SELECT * FROM kullanicilar WHERE yas NOT IN (16,21)
```
Sorgu'da yaşı *16 ve 21* olan kullanıcıları getirmez.

#### DISTINCT
`DISTINCT`, örnek bir tabloda aynı kayıttan birden fazla kayıt ve sadece 1 tane çekmek istiyoruz bunun için `DISTINCT` kullanabiliriz.
```SQL
    SELECT DISTINCT (yas) isim, soyisim FROM kullanicilar WHERE yas = 21
```
Burda sadece `isim` ve `soyisim` kolonlarını döndürecek. Tüm kolonlar için `ON` kullanmanız gerekecek. `SELECT DISTINCT ON ('kolon_adi') * WHERE ..`
```SQL 
  SELECT DISTINCT ON (yas) * FROM kullanicilar WHERE yas = 21
```
#### LIMIT
`LIMIT`, bir tablodan veri çekerken belli bir sayıda kayıt döndürmek için kullanılır. 
```SQL 
  SELECT * FROM kullanicilar LIMIT 25
```
Bu sorguda kullanıcılar tablosundan 25 kayıt döndürecek. 

#### OFFSET
`OFFSET`, nerden başlayacağını belirtmek için kullanılır. Mesela 50. kayıttan sonrakileri çekmek istiyoruz
```SQL 
  SELECT * FROM kullanicilar LIMIT 100 OFFSET 50
```
50'den başlayıp 100 tane kayıt döndürecek.