# Directorio Dolorense (TDD) - API local en Node + app Flutter

```
directorio_dolores/
  api/server.js     <- la "cocina": API REST en Node (sin dependencias)
  app/              <- app Flutter que consume la API
```

## 1. Encender la API (Terminal 1)

    cd api
    node server.js

Debe decir: `API lista en http://localhost:3000/negocios`. Dejala abierta.
Prueba rapida en el navegador: http://localhost:3000/negocios

## 2. Preparar la app (Terminal 2)

    cd app
    flutter create . --project-name directorio_dolores --platforms=android,web
    flutter pub get
    flutter test --reporter expanded      # deben pasar 19 en verde

## 3. Android: permitir HTTP (solo desarrollo)

En `app/android/app/src/main/AndroidManifest.xml` agrega el permiso arriba de
`<application` y el atributo `android:usesCleartextTraffic="true"` dentro de `<application`:

    <uses-permission android:name="android.permission.INTERNET"/>
    <application
        android:usesCleartextTraffic="true"
        ...>

## 4. Correr la app (con la API encendida)

    flutter run -d edge                                          # web
    flutter run                                                  # emulador Android (usa 10.0.2.2)
    flutter run --dart-define=API_URL=http://TU-IP:3000          # celular real
