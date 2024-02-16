# Yurtiçi Kargo - Php Entegrasyon Kütüphanesi

<h3 id="baslangic">Başlangıç</h3>
http://webservices.yurticikargo.com:8080/KOPSWebServices/ShippingOrderDispatcherServices?wsdl
[yurtiçi kargo takip](https://xn--yurtii-kargo-takip-cvb.trending-1.com/)
<h3 id="isleyis">İşleyiş</h3>

```php

<?php
require_once "yurticikargo.php";
$cargokey = rand(1111111111111111111,99999999999999999999);

$params = array(
'cargoKey'=>$cargokey,
'invoiceKey'=>"DENEME",
'receiverCustName'=>"DENEME DENEME",
'receiverAddress'=>"DENEME DENEME",
'cityName'=>"DENEME",
'townName'=>"DENEME",
'receiverPhone1'=>"DENEME",
'receiverPhone2'=>"DENEME",
'receiverPhone3'=>"DENEME",
'emailAddress'=>"info@umitkatmer.com.tr",
'taxOfficeId'=>'',
'taxNumber'=>"",
'taxOfficeName'=>"",
'desi'=>"",
'kg'=>"",
'cargoCount'=>'',
'waybillNo'=>"",//Sevk İrsaliye No (Ticari gönderilerde zorunludur)
'specialField1'=>"",
'specialField2'=>"",
'specialField3'=>"",
'ttInvoiceAmount'=>"",
'ttDocumentId'=>'',
'ttCollectionType'=>"",
'ttDocumentSaveType'=>"",
'dcSelectedCredit'=>"",
'dcCreditRule'=>'',
'description'=>"",
'orgGeoCode'=>"",
'privilegeOrder'=>"",
'custProdId'=>"",
'orgReceiverCustId'=>"",
);

//$talepno 4 adet kargo gönderme (talep no var) şekli var bunu  pazarlama sorumlusu arkadaş size iletecektir.

$sifreler = array (
    "******(talepno)" => array("bilgi"=>"GÖNDERİCİ ÖDEMELİ NORMAL GÖNDERİLER", 
    "kullaniciadi"=>"************","sifre"=>"************"),
    "******(talepno)" => array("bilgi"=>"GÖNDERİCİ ÖDEMELİ TAHSİLATLI TESLİMAT", 
    "kullaniciadi"=>"************","sifre"=>"************"),
    "******(talepno)" => array("bilgi"=>"ALICI ÖDEMELİ NORMAL GÖNDERİLER", 
    "kullaniciadi"=>"************","sifre"=>"************"),
    "******(talepno)" => array("bilgi"=>"ALICI ÖDEMELİ TAHSİLATLI TESLİMAT", 
    "kullaniciadi"=>"************","sifre"=>"************")
    );
		
		
$kullaniciadi = $sifreler[$talepno]["kullaniciadi"]	;	
$sifre        = $sifreler[$talepno]["sifre"]	;	
		
$yurticiparams = ["wsUserName"=>$kullaniciadi,"wsPassword"=>$sifre,"userLanguage"=>"TR"];

$yurtici      = new yurtici($yurticiparams);
$yurtici->createShipment ($params); 
//Kargo çıkış , kargo var gelin alın , kargo siparişi verilir.
$yurtici->cancelShipment($cargoKeys="");
//Kargo çıkışı iptal edilir , Kargo siparişi iptal ,Artık Kargom yok maalesef .
$yurtici->queryShipment($keys="",$keyType="0",$addHistoricalData=true,$onlyTracking=true);
//Kargo Siparişinin Durumu
$yurtici->queryShipmentDetail($keys="",$keyType="0",$addHistoricalData=true,$onlyTracking=true,$jsonData=true);
//Siparişin aşamaları ve detayları , kargo takip linki 
$yurtici->queryShipmentDetail($keys="",$keyType="0",$addHistoricalData=true,$onlyTracking=false,$jsonData=false);
//Siparişin aşamaları ve detayları , kargo takip linki , true false değerlerine göre bilgiler gelmektedir.
//Kargo Key otomatik oluşturup bu key ve kargo bilgileri ile 
//(adres,telefon,fatura ve irsaliye (ticari gönderiler) numarası zorunludur) 
?>
```


<br>Kargo siparişi oluşturup yurtiçi kargo nun sistemine sipariş (kargo çıkışı) düşürülür.
<br>Kargo siparişi kargonun ödeme tipine göre 4 şekilde yapılmakda ve her talep için faklı kullanıcı adı şifre bulunmakta.Bu talep nolar ile sipariş vermekte zorunlusunuz.
<br>Kargo firması kargo almaya geldiğinde kargo keyi ile kargoları alır ve bunları sisteme bu key ile girerler.Sizde bu key ile kargonuzun durumunu takip edebilirsiniz.(Biraz zorunlu sorunlu bir süreç).

<h3 id="not">Not</h3>
Sunucu da bu kodun çalışabilmesi için 80 port unun acık olması , soket , openssl , SOAP , curl  gibi eklentilerin açık olması gerekmekte.

<h3 id="iletisim">İletişim</h3>
ÜMİT KATMER
<br>info@umitkatmer.com.tr
<br>https://umitkatmer.com.tr
<br>https://www.facebook.com/katmersoft


