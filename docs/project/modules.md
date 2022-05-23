## Modules

### Global Module

Varsayılan olarak, yeni bir TypeScript dosyasına kod yazmaya başladığınızda, kodunuz genel bir *global* Aduzayındadır. Bir demo olarak, bir `foo.ts` dosyasını düşünün:

```ts
var foo = 123;
```

Şimdi aynı projede *yeni* bir `bar.ts` dosyası oluşturursanız, TypeScript'in tür sistemi tarafından 'foo' değişkenini küresel olarak kullanmanıza *izin verir*:

```ts
var bar = foo; // Geçerli
```
Needless to say having a global namespace is dangerous as it opens your code up for naming conflicts. We recommend using file modules which are presented next.
Genel bir Aduzayı alanına sahip olmanın tehlikeli olduğunu söylemeye gerek yok çünkü kodunuzu isimlendirme çakışmaları için açıyor. Daha sonra sunulan dosya modüllerini kullanmanızı öneririz.

### File Module - Dosya Modülü
Also called *external modules*. If you have an `import` or an `export` at the root level of a TypeScript file then it creates a *local* scope within that file. So if we were to change the previous `foo.ts` to the following (note the `export` usage):

Ayrıca *harici modüller* olarak da adlandırılır. TypeScript dosyasının kök düzeyinde bir `import` veya `export` işleminiz varsa, bu dosya içinde *yerel* bir kapsam oluşturur. Öyleyse, önceki `foo.ts` dosyasını aşağıdaki gibi değiştirecek olursak (`export` kullanımına dikkat edin):

```ts
export var foo = 123;
```

Global AdUzayı alanında artık `foo` olmayacak. Bu, aşağıdaki gibi yeni bir `bar.ts` dosyası oluşturarak gözlemlenebilir:

```ts
var bar = foo; // ERROR: "cannot find name 'foo'" - HATA: "'foo' adı bulunamıyor"
```

If you want to use stuff from `foo.ts` in `bar.ts` *you need to explicitly import it*. This is shown in an updated `bar.ts` below:

Eğer  `bar.ts` içerisinde `foo.ts` dosyasındaki bir şeyleri kullanmak istiyorsanız *açıkça içe aktarmanız gerekir*. Bu, aşağıda güncellenmiş bir `bar.ts` dosyası içerisinde gösterilmiştir:

```ts
import {foo} from "./foo";
var bar = foo; // Geçerli
```

`bar.ts` içinde bir `import` kullanmak sadece diğer dosyalardan bir şeyler çağırmanıza izin vermekle kalmaz, aynı zamanda `foo.ts` dosyasını bir *module* olarak işaretler. Bu nedenle `foo.ts` dosyası veya global AdUzayı bozulmaz. 

Harici modülleri kullanan belirli bir TypeScript dosyasından oluşturulan JavaScript, `module` adlı derleyici bayrağı tarafından yönlendirilir.
