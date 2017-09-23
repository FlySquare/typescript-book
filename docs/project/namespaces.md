## Aduzayları (Namespaces)
Aduzayları, JavaScript'te kullanılan yaygın bir kalıp için uygun sözdizimi sağlar:  

```ts
(function(something) {

    something.foo = 123;

})(something || something = {})
```
Basit olarak anlatmak gerekirse `something || something = {}` ifadesi, anonim fonksiyonun *varolan bir nesneye eklenti yapmasını* (`something ||` kısmı) veya *yeni bir obje yaratarak yaratılan bu yeni objeye eklenti yapılmasına* (`|| something = {}` kısmı) imkan tanır.
Bunun anlamı şudur, bir çalıştırma sınırıyla ayrılmış iki farklı kod bloğuna sahip olabilirsiniz:


```ts
(function(something) {

    something.foo = 123;

})(something || something = {})

console.log(something); // {foo:123}

(function(something) {

    something.bar = 456;

})(something || something = {})

console.log(something); // {foo:123, bar:456}

```
Javascript'te bunun en yaygın kullanım amacı global(küresel) aduzayına bilgi sızmasını önlemektir. Dosya tabanlı modüller kullanıldığında bu konu hakkında endişe etmenize gerek olmamakla birlikte, bu kalıp fonksiyonlarınızı *mantıksal olarak gruplamak* için oldukça kullanışlıdır. Bu tip gruplamaları yapabilmeniz için TypeScript `namespace` anahtar kelimesini sunmaktadır. Ör:

```ts
namespace Utility {
    export function log(msg) {
        console.log(msg);
    }
    export function error(msg) {
        console.error(msg);
    }
}

// usage
Utility.log('Call me');
Utility.error('maybe!');
```
`namespace` anahtar kelimesi ilk bölümde gördüğümüz JavaScript kodunun aynısını üretmektedir.

```ts
(function (Utility) {

// Add stuff to Utility

})(Utility || (Utility = {}));
```
Bir diğer nokta ise, uzayadları iç içe geçebilirler, bu sayede `namespace Utility.Messaging` gibi bir ifadeyle `Messaging` uzayadını `Utility` uzayadının içine tanımlamak mümkün olmaktadır.

Örnek proje oluştururken veya eski JavaScript kodunu port ederken  harici modül ve `namespace` kullanımı tavsiye edilmektedir.
