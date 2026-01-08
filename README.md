# 📦 Amazon Sipariş İade Tahminlemesi ve Analizi

Bu proje, Amazon sipariş verilerini kullanarak bir ürünün iade edilip edilmeyeceğini sipariş anında tahmin eden bir Makine Öğrenmesi projesidir. 
Çalışmada Dengesiz Veri (Imbalanced Data) problemi üzerinde durulmuş, Undersampling tekniği ve XGBoost algoritması kullanılarak iade yakalama başarısı optimize edilmiştir.

## 🎯 Projenin Amacı
E-ticaret operasyonlarında iadeler, lojistik maliyetlerini artıran ve kârlılığı düşüren en büyük risklerden biridir.
Problem: Veri setindeki siparişlerin %96'sı başarılı teslimat, sadece %3.92'si iadedir. 
Standart modeller bu dengesizlik nedeniyle iadeleri tahmin edememektedir (Accuracy Paradox).
Hedef: Genel doğruluktan (Accuracy) ziyade, İade Yakalama Başarısını (Recall) maksimize ederek proaktif önlem alınmasını sağlamak.

## 📊 Veri Seti ve Özellik Mühendisliği (Feature Engineering)
* **Veri Seti:** Amazon satış verileri (Sipariş tarihi, tutarı, kargo maliyeti, ürün kategorisi, lokasyon vb.)
* **Veri Boyutu:** ~77.000 Satır
* **Hedef Değişken:** IsReturned (1: İade, 0: Teslim)
* **Türetilen Özellikler:**
ShippingRatio: Kargo maliyetinin toplam sipariş tutarına oranı hesaplanarak, müşterinin "maliyet hassasiyeti" modele kazandırılmıştır.
Month & DayOfWeek: Sipariş tarihinden ay ve gün bilgisi türetilerek mevsimsellik etkisi yakalanmıştır.

## ⚙️ Kullanılan Yöntemler
Bu projede veri sızıntısını önlemek ve model başarısını artırmak için şu adımlar izlenmiştir:
  1. **Veri Ön İşleme:** Eksik verilerin yönetimi, Label Encoding ve Stratified Train-Test Split (%70-%30).
  2. **Dengesiz Veri Çözümü:** RandomUnderSampler kullanılarak sadece eğitim seti 1:1 oranında dengelenmiştir (Majority Class azaltılmıştır).
  3. **Modeller:** Random Forest: Baseline (Baz) model olarak kullanıldı.
                   XGBoost: Challenger (Rakip) model olarak kullanıldı ve optimize edildi.

## 🚀 Sonuçlar ve Karşılaştırma     
Yapılan testler sonucunda XGBoost algoritması, Random Forest'a göre daha yüksek başarı göstermiştir.

<img width="768" height="287" alt="image" src="https://github.com/user-attachments/assets/fcb610c1-763f-49c8-a23a-2ab0b22fdb2c" />
Not: Eğitim seti dengelendiği için modelin genel doğruluğu (Accuracy) düşmüştür. Ancak bu bilinçli bir "Trade-off"tur. Bu sayede ham veriyle %0 olan iade yakalama oranı %53'e çıkarılmıştır.

<img width="626" height="470" alt="image" src="https://github.com/user-attachments/assets/d3966c5d-509b-4a47-a4bb-41043dac0ca6" />
<img width="894" height="513" alt="image" src="https://github.com/user-attachments/assets/f489c0ee-6b67-47b2-9697-c02a0189734b" />



