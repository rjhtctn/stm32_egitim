\# 02. GPIO Giriş Uygulaması: Buton Durumu Okuma (Digital Input)



Bu proje, \*\*STM32F303RE\*\* mikrodenetleyicisinde bir GPIO pininin "Input" (Giriş) olarak kullanılmasını ve pinin lojik durumunun (0 veya 1) okunmasını gösterir.



Uygulamada, Nucleo kartı üzerindeki \*\*Mavi Kullanıcı Butonu (B1)\*\* durumu okunarak bir değişkene aktarılmaktadır. Bu proje, \*\*Debug modunda değişken takibi (Live Expressions)\*\* özelliğini öğrenmek için tasarlanmıştır.



!\[Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)

!\[Peripheral](https://img.shields.io/badge/Peripheral-GPIO\_Input-blue)



\## ⚙️ Donanım Bağlantıları



| Pin | Etiket | Donanım | Açıklama |

| :--- | :--- | :--- | :--- |

| \*\*PC13\*\* | `B1\_Pin` | \*\*User Button (Mavi)\*\* | Giriş Pini (Input) |



\## 📝 Yazılım Mantığı



1\.  \*\*Değişken Tanımlama:\*\* Butonun durumunu saklamak için global bir `uint8\_t butonDurumu` değişkeni oluşturulmuştur (Varsayılan: 1).

2\.  \*\*GPIO Okuma (`HAL\_GPIO\_ReadPin`):\*\*

&nbsp;   \* Ana döngü (`while(1)`) içerisinde sürekli olarak \*\*PC13\*\* portunun durumu okunur.

&nbsp;   \* Butona basıldığında veya bırakıldığında pinin lojik seviyesi (SET/RESET) değişkene anlık olarak yazılır.



```c

/\* Ana döngü içerisindeki okuma işlemi \*/

while (1)

{

&nbsp; // GPIOC portunun 13. pinini oku ve sonucu değişkene ata

&nbsp; butonDurumu = HAL\_GPIO\_ReadPin(GPIOC, GPIO\_PIN\_13);

}

