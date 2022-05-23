### Basic
İhtiyacınız olan temel dosya tsconfig.json olduğundan, kullanmaya başlamak son derece kolaydır:
```json
{}
```
Yani projenizin *kök dizininde* boş bir JSON dosyasıdır. Bu şekilde TypeScript, derleme bağlamının bir parçası olarak bu dizindeki (ve alt dizinlerdeki) `.ts` dosyalarının *tümünü* içerecektir. Ayrıca birkaç varsayılan derleyici seçeneğini seçecektir.

### compilerOptions
Derleyici seçeneklerini `compilerOptions` kullanarak özelleştirebilirsiniz.

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "declaration": false,
        "noImplicitAny": false,
        "removeComments": true,
        "noLib": false
    }
}
```

Bu (ve daha fazla) derleyici seçenekleri daha sonra tartışılacaktır.

### TypeScript compiler
Modern Geliştirici Ortamları(IDE) `ts` ve `js` derlenmesi için yerleşik bir destekle birlikte gelmektedir. Ancak TypeScript derleyicisini `tsconfig.json` kullanırken komut satırından manuel olarak çalıştırmak istiyorsanız, bunu birkaç yolla yapabilirsiniz.
* Sadece `tsc`'yi çalıştırın. Dosyayı bulana kadar tüm ana klasörlerde ve mevcut klasörde `tsconfig.json`'u arayacaktır.
* `tsc -p ./path-to-project-directory` komutunu çalıştırın. Belirtilen yol, tam veya geçerli dizin olmalıdır.

Hatta TypeScript derleyicisini `tsc -w` kullanarak *watch* - *izleme* modunda başlatabilirsiniz ve bu mod, değişiklikler için TypeScript proje dosyalarınızı izleyecektir.
