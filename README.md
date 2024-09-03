# MDP Group
## Flutter Case Study

Bu uygulama, Giriş, Ana Sayfa ve Ürün Listeleme olmak üzere üç ana sayfadan oluşmaktadır. Amaç, bu ekranları kullanarak basit bir e-ticaret uygulaması prototipi oluşturmaktır.

[Figma Projesi](https://www.figma.com/design/IG2V5YNceAvhRr6brJ7x8b/Flutter-Case-Study?node-id=0-1&m=dev&t=ZJvxwD567mVsZBqW-1)

#### 1. **Giriş Ekranı**
- Giriş ekranında kullanıcı adı ve şifre alanları bulunacaktır.
- Bir "Beni Hatırla" seçeneği olmalıdır. Seçildiğinde, kullanıcı bir dahaki sefere uygulamayı açtığında alanlar otomatik olarak doldurulacaktır.
- Kullanıcı girişi için aşağıdaki gibi bir istek yapılacaktır:

```javascript
fetch('https://dummyjson.com/auth/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    username: 'emilys',
    password: 'emilyspass',
    expiresInMins: 30 // opsiyonel, varsayılan 60 dakika
  })
})
.then(res => res.json())
.then(console.log);
```

- Yanıt olarak aşağıdaki gibi bir JSON dönecektir:

```json
{
  "id": 1,
  "username": "emilys",
  "email": "emily.johnson@x.dummyjson.com",
  "firstName": "Emily",
  "lastName": "Johnson",
  "gender": "female",
  "image": "https://dummyjson.com/icon/emilys/128",
  "token": "eyJhbGciOiJIUz...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIs..."
}
```

#### 2. **Ana Sayfa**
- Kullanıcı bilgileri bir kart içinde listelenecektir. Giriş işlemi sırasında alınan veriler bu kartta gösterilecektir.
- Kullanıcı bilgileri kartının altında, "Popüler Ürünler" başlığı altında yatay bir ürün listeleme bölümü yer alacaktır. Maksimum 10 ürün gösterilecektir.
- "Tümünü Gör" butonuna tıklandığında, kullanıcı Ürün Listeleme sayfasına yönlendirilecektir.
- Popüler ürünler için istek aşağıdaki gibi yapılacaktır:

```javascript
fetch('https://dummyjson.com/products?limit=10')
.then(res => res.json())
.then(console.log);
```

- Yanıt olarak ilk 10 ürünün listelendiği bir JSON dönecektir:

```json
{
  "products": [
    {
      "id": 1,
      "title": "Essence Mascara Lash Princess",
      "price": 9.99,
      // diğer ürün bilgileri...
    },
    {...},
    {...},
    // toplamda 10 ürün
  ],
  "total": 100,
  "skip": 0,
  "limit": 10
}
```

#### 3. **Ürün Listeleme Sayfası**
- Ürünler, sayfalama yapısı kullanılarak listelenecektir. Limit 10 olarak ayarlanacak ve sonsuz kaydırma ile her seferinde 10 adet ürün yüklenecek.
- Ürün listeleme isteği aşağıdaki gibi yapılacaktır:

```javascript
fetch('https://dummyjson.com/products?limit=10&skip=10&select=title,price')
.then(res => res.json())
.then(console.log);
```

- Yanıt olarak aşağıdaki gibi bir JSON dönecektir:

```json
{
  "products": [
    {
      "id": 11, // ilk 10 ürün atlandı
      "title": "Annibale Colombo Bed",
      "price": 1899.99
    },
    {...},
    {...},
    // toplamda 10 ürün
  ],
  "total": 194,
  "skip": 10,
  "limit": 10
}
```

- Bir ürün kartına tıklandığında, bir modal açılacak ve bu modalda text girişi yapılabilen bir alan yer alacaktır. Girilen text ile aşağıdaki endpoint'e istek atılacak ve dönen yanıt snackbar ile gösterilecektir:

```javascript
fetch('https://dummyjson.com/products/1', {
  method: 'PUT', /* veya PATCH */
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    title: 'iPhone Galaxy +1'
  })
})
```

#### 4. **Profil Sayfası**
- Aktif kullanıcı bilgilerini görüntüleyen bir sayfa olacaktır.
- Bu sayfa üzerinden dil değişikliği yapılabilecek (Türkçe/İngilizce).
- Ayrıca bir "Çıkış Yap" butonu da yer alacak. Bu butona tıklandığında kullanıcı Giriş ekranına geri dönecektir.

---

Bu talimatlar ve örnekler kullanılarak, stajyerinizin Flutter ile uygulamayı geliştirmesi beklenmektedir. Görseller, kullanıcı arayüzünün nasıl görüneceği konusunda rehberlik edecektir.

#### 1. **Giriş Ekranı**
- Giriş ekranında kullanıcı adı ve şifre alanları bulunacaktır.
- Bir "Beni Hatırla" seçeneği olmalıdır. Seçildiğinde, kullanıcı bir dahaki sefere uygulamayı açtığında alanlar otomatik olarak doldurulacaktır.
- Kullanıcı girişi için aşağıdaki gibi bir istek yapılacaktır:

```javascript
fetch('https://dummyjson.com/auth/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    username: 'emilys',
    password: 'emilyspass',
    expiresInMins: 30 // opsiyonel, varsayılan 60 dakika
  })
})
.then(res => res.json())
.then(console.log);
```

- Yanıt olarak aşağıdaki gibi bir JSON dönecektir:

```json
{
  "id": 1,
  "username": "emilys",
  "email": "emily.johnson@x.dummyjson.com",
  "firstName": "Emily",
  "lastName": "Johnson",
  "gender": "female",
  "image": "https://dummyjson.com/icon/emilys/128",
  "token": "eyJhbGciOiJIUz...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIs..."
}
```

#### 2. **Ana Sayfa**
- Kullanıcı bilgileri bir kart içinde listelenecektir. Giriş işlemi sırasında alınan veriler bu kartta gösterilecektir.
- Kullanıcı bilgileri kartının altında, "Popüler Ürünler" başlığı altında yatay bir ürün listeleme bölümü yer alacaktır. Maksimum 10 ürün gösterilecektir.
- "Tümünü Gör" butonuna tıklandığında, kullanıcı Ürün Listeleme sayfasına yönlendirilecektir.
- Popüler ürünler için istek aşağıdaki gibi yapılacaktır:

```javascript
fetch('https://dummyjson.com/products?limit=10')
.then(res => res.json())
.then(console.log);
```

- Yanıt olarak ilk 10 ürünün listelendiği bir JSON dönecektir:

```json
{
  "products": [
    {
      "id": 1,
      "title": "Essence Mascara Lash Princess",
      "price": 9.99,
      // diğer ürün bilgileri...
    },
    {...},
    {...},
    // toplamda 10 ürün
  ],
  "total": 100,
  "skip": 0,
  "limit": 10
}
```

#### 3. **Ürün Listeleme Sayfası**
- Ürünler, sayfalama yapısı kullanılarak listelenecektir. Limit 10 olarak ayarlanacak ve sonsuz kaydırma ile her seferinde 10 adet ürün yüklenecek.
- Ürün listeleme isteği aşağıdaki gibi yapılacaktır:

```javascript
fetch('https://dummyjson.com/products?limit=10&skip=10&select=title,price')
.then(res => res.json())
.then(console.log);
```

- Yanıt olarak aşağıdaki gibi bir JSON dönecektir:

```json
{
  "products": [
    {
      "id": 11, // ilk 10 ürün atlandı
      "title": "Annibale Colombo Bed",
      "price": 1899.99
    },
    {...},
    {...},
    // toplamda 10 ürün
  ],
  "total": 194,
  "skip": 10,
  "limit": 10
}
```

- Bir ürün kartına tıklandığında, bir modal açılacak ve bu modalda text girişi yapılabilen bir alan yer alacaktır. Girilen text ile aşağıdaki endpoint'e istek atılacak ve dönen yanıt snackbar ile gösterilecektir:

```javascript
fetch('https://dummyjson.com/products/1', {
  method: 'PUT', /* veya PATCH */
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    title: 'iPhone Galaxy +1'
  })
})
```

#### 4. **Profil Sayfası**
- Aktif kullanıcı bilgilerini görüntüleyen bir sayfa olacaktır.
- Bu sayfa üzerinden dil değişikliği yapılabilecek (Türkçe/İngilizce).
- Ayrıca bir "Çıkış Yap" butonu da yer alacak. Bu butona tıklandığında kullanıcı Giriş ekranına geri dönecektir.
