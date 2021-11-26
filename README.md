# n11-case-study

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Project Description
ES6 kullanarak Vue.js framework'ü ile basit bir ürün detay sayfası yapılmıştır.     
Sayfa 3 parçadan oluşuyor, detaylandıracak olursak;



Bu ürün detay sayfasının sol tarafında büyük görsel ve altında thumbnail görsellerinin  
olduğu bir görsel alanı olacak. Küçük resimlere tıkladıkça üst taraftaki büyük görsel  
değişecek.


Sağ tarafta ürüne ait opsiyonlar gösterilecek. Renk/Beden gibi. Hangi rengi seçerse  
o renge ait bedenler gösterilecek, eğer bedenlerden olmayan varsa pasif olarak  
gösterilecek. Örneğin opsiyonlardan siyah rengi seçti ve o renkte sadece M beden varsa  
diğer bedenler seçilemez olarak gösterilecek.


Toptan Fiyat/Adet barem aralığı: Adet aralığını ve ona göre fiyatını gösterir  
barem aralığı alanı ile kullanıcının almak istediği ürün adedini girebileceği  
number input alanı vardır. Datadaki barem aralığı baz alınarak kullanıcının  
girmiş olduğu sayıya göre seçili barem aralığı değişecek.  
Bu alan tıklanabilir bir alan değildir, kullanıcının girdiği adet sayısına denk gelen  
barem aralığının gösterimi içindir.  


İlk başta tüm görseller görünür olur. Her bir variant’ın görseli datada mevcuttur.  
Seçili opsiyona göre ilgili görseller görünürdür.   
Örneğin Siyah renk / L beden seçimi yaptı, onun görselleri ne ise sadece onlar  
görünmektedir.  


Sepete Ekle butonu tüm seçimler yapıldıktan sonra disable’dan enable  
konuma gelir. Nihai datayı kontrol edebilmek için buton enable konuma  
geldikten sonra seçili olan attribute’un id'sini ve seçili baremi  
console’a basılmaktadır.  

Bu Çözüm Yalnızca Belirtilen mock-up-data için özel olarak geliştirilmiştir.
