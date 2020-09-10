### İçerikler
* [SELECT](#select)
* [FROM](#from)
* [WHERE](#where)
* [AS](#as)
* [LIKE](#like)
* [ORDER](#order-by)

Bir veya birden fazla tablodan satırları çeker.
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
    SELECT isim AS ad FROM kullaniclar WHERE yas > 21
```

#### LIKE 
`LIKE`, kolonlar üzerinde arama yapmamıza olanak sağlıyor. Kullanıma geçelim.

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