# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

# Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

## Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#Tablolar 
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/] (update, delete, drop sorguları iptal edilmiştir).

### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını altlarına yazın. 


	1) ÖRNEK SORU: Öğrenci tablosundaki tüm kayıtları listeleyin.
	
		CEVAP: select * from ogrenci

	
	2) Öğrenci tablosundaki öğrencinin adını ve soyadını ve sınıfını listeleyin.
	
	CEVAP: select ograd, ogrsoyad, sinif from ogrenci order by sinif;
	
	3) Öğrenci tablosundaki kız öğrencileri listeleyin. 
	
	CEVAP: select * from ogrenci where cinsiyet = 'K';
	
	4) Öğrenci tablosunda kaydı bulunan sınıfların adını her sınıf bir kez görüntülenecek şekilde listeleyiniz
	
	CEVAP: select distinct sinif from ogrenci order by sinif;
	
	5) Öğrenci tablosunda, 10A sınıfında olan kız öğrencileri listeleyiniz.
	
	 CEVAP: select * from ogrenci where cinsiyet = 'K' and sinif = '10A';

	6) Öğrenci tablosundaki 10A veya 10B sınıfındaki öğrencilerin adını, soyadını ve sınıfını listeleyiniz.
	
	CEVAP: select ograd, ogrsoyad, sinif from ogrenci where sinif = '10A' or sinif = '10B';

    select concat(ograd,' ',ogrsoyad,'(',cinsiyet,')') as adsoyad, sinif from ogrenci where sinif in('10A', '10B') and trim(concat(ograd,' ',ogrsoyad,'(',cinsiyet,')')) is not null order by sinif;


	7) Öğrenci tablosundaki öğrencinin adını, soyadını ve numarasını okul numarası olarak listeleyiniz. (as kullanım örneği)
	
	CEVAP: select ograd, ogrsoyad, ogrno from ogrenci;

	8) Öğrenci tablosundaki öğrencinin adını ve soyadını birleştirip, adsoyad olarak listeleyiniz. (concat, as kullanım örneği)
	
	CEVAP: select concat(ograd,' ',ogrsoyad) as adsoyad from ogrenci;

	select DISTINCT concat(ograd,' ',ogrsoyad) as adsoyad, sinif, dtarih from ogrenci where sinif IN('9A', '9C') AND ograd LIKE '%A%' order by concat(ograd,' ',ogrsoyad), dtarih DESC LIMIT 5;
	
	9) Öğrenci tablosundaki Adı ‘A’ harfi ile başlayan öğrencileri listeleyiniz.
	
	CEVAP: select * from ogrenci where ograd like 'A%';
	
	10) Kitaplar tablosundaki sayfa sayısı 50 ile 200 arasında olan kitapların adını ve sayfa sayısını listeleyiniz.

    CEVAP: select kitapadi, sayfasayisi from kitap where sayfasayisi >=50 and sayfasayisi <=200 order by sayfasayisi;

	11) Öğrenci tablosunda adı Fidan, İsmail ve Leyla olan öğrencileri listeleyiniz.
	
	CEVAP: select * from ogrenci where ograd in('Fidan', 'İsmail', 'Leyla');
	
	12) Öğrenci tablosundaki öğrencilerden adı A, D ve K ile başlayan öğrencileri listeleyiniz.
	
	CEVAP: select * from ogrenci where ograd LIKE 'A%' or ograd LIKE 'D%' or ograd LIKE 'K%';
	
	13) Öğrenci tablosundaki sınıfı 9A olan Erkekleri veya sınıfı 9B olan kızların adını, soyadını, sınıfını ve cinsiyetini listeleyiniz.
	
	CEVAP: select ograd, ogrsoyad, sinif, cinsiyet from ogrenci where sinif = '9A' and cinsiyet = 'E' or sinif = '9B' and cinsiyet = 'K' order by cinsiyet;
	
	14) Sınıfı 10A veya 10B olan erkekleri listeleyiniz.
	
	CEVAP: select * from ogrenci where cinsiyet = 'E' and sinif = '10A' or sinif = '10B' order by sinif;
	
	15) Öğrenci tablosunda doğum yılı 1989 olan öğrencileri listeleyiniz.
	
	CEVAP:  select * from ogrenci where dtarih = 1989 order by dtarih;
	
	16) Öğrenci numarası 30 ile 50 arasında olan Kız öğrencileri listeleyiniz.
	
	CEVAP: select * from ogrenci where ogrno >=30 and ogrno <=50 and cinsiyet = 'K' order by ogrno;
	
	17) Öğrencileri adına göre sıralayınız (alfabetik).
	
	CEVAP: select * from ogrenci order by ograd;
	
	18) Öğrencileri adına, adı aynı olanlarıda soyadlarına göre sıralayınız.
	
	CEVAP: select * from ogrenci order by ograd, ogrsoyad;
	
	19) 10A sınıfındaki öğrencileri okul numarasına göre azalan olarak sıralayınız.
	
	CEVAP: select * from ogrenci where sinif = '10A' order by ogrno desc;
	
	20) Öğrenciler tablosundaki ilk 10 kaydı listeleyiniz.
	[İPUCU: `select top tüm mysql versiyonlarında düzgün çalışmaz. LİMİT kullanmak daha faydalıdır`]
	
    CEVAP: select * from ogrenci LIMIT 10;

	21) Öğrenciler tablosundaki ilk 10 kaydın ad, soyad ve doğum tarihi bilgilerini listeleyiniz.
	
	CEVAP: select ograd, ogrsoyad, dtarih from ogrenci LIMIT 10;
	
	22) Sayfa sayısı en fazla olan kitabı listeleyiniz.
	
	CEVAP: select * from kitap ORDER BY sayfasayisi DESC LIMIT 1;
	
	23) Öğrenciler tablosundaki en genç öğrenciyi listeleyiniz.
	
	CEVAP: select * from ogrenci ORDER BY dtarih ASC LIMIT 1;
	
	24) 10A sınıfındaki en yaşlı öğrenciyi listeyin.
	
	CEVAP: select * from ogrenci where sinif = '10A' ORDER BY dtarih DESC LIMIT 1;
	
	25) İkinci harfi N olan kitapları listeleyiniz.
	
	CEVAP: select * from kitap where kitapadi LIKE '_N%';
	
	26) Öğrencileri sınıflarına göre gruplayarak listeleyin.
	
	CEVAP: select * from ogrenci ORDER BY sinif;
	
	27) Öğrencileri her sorgulamada sıralaması farklı olacak şekilde rastgele listeleyin. 
	[İPUCU: rand() fonksiyonu]
	
	CEVAP: select * from ogrenci ORDER BY RAND();
	
	28) Öğrenci tablosundan Rastgele bir öğrenci seçiniz.
	
	CEVAP: select * from ogrenci ORDER BY RAND() LIMIT 1;
	
	29) 10A sınıfından rastgele bir öğrencinin adını, soyadını, numarasını ve sınıfını getirin.
	
	CEVAP: select ograd, ogrsoyad, ogrno, sinif from ogrenci where sinif = '10A' ORDER BY RAND() LIMIT 1;
	
	# Esnek
	30) Öğrenci tablosunda aynı isimde kaçar öğrenci olduğunu bulmak istiyoruz. 
	Öğrenci isimlerinin sayısını "adet" olarak öğrencilerin isimleri "isim" olarak listeleyin. 
	[İPUCU: count() ve group by]

    CEVAP: select COUNT(*) as adet, ograd as isim from ogrenci GROUP BY ograd;