# Delivery Client - App Móvil de Delivery Multi-Restaurante

## 📋 Descripción

Aplicación móvil completa de food delivery desarrollada en Flutter que permite a usuarios explorar restaurantes, ordenar comida, gestionar carrito de compras y rastrear pedidos en tiempo real. Integrada con backend Laravel, soporta múltiples métodos de pago, ubicaciones GPS y notificaciones push.

**Versión:** 1.8.0 (Build 2)

## 🚀 Tipo de Proyecto

**Aplicación Móvil Multiplataforma** - Food Delivery Client (iOS + Android)

## 🛠️ Stack Tecnológico

**Framework:**
- Flutter (Dart 2.1.0 - 3.0.0)
- Dart Language
- MVC Pattern (mvc_pattern ^3.4.1)

**State Management:**
- ValueNotifier para estado reactivo
- StateMVC para páginas
- ControllerMVC para lógica de negocio
- SharedPreferences para persistencia

**Integración Backend:**
- API REST (Laravel backend)
- Base URL: carrosautoparts.com/datos/delivery/public/

## 📚 Frameworks y Librerías

**Core:**
```yaml
mvc_pattern: ^3.4.1          # Arquitectura MVC
global_configuration: ^1.3.0  # Configuración global
http: ^0.12.0+2              # Cliente HTTP

Firebase:
firebase_messaging: ^6.0.13   # Push notifications
firebase_analytics: ^5.0.11   # Event tracking

UI & Theming:
dynamic_theme: ^1.0.0         # Dark/Light themes
flutter_svg: ^0.14.2          # SVG support
cached_network_image: 2.0.0   # Image caching
flutter_html: ^0.10.4         # HTML rendering
flutter_swiper: ^1.1.6        # Carousel widget

Maps & Location:
google_maps_flutter: ^0.5.21+8  # Google Maps
location: ^2.3.5                # GPS services

Payments:
flutter_inappbrowser: ^1.2.2  # In-app browser
url_launcher: ^5.4.1          # External URLs

Utilities:
intl: ^0.16.0                 # Internationalization
shared_preferences: ^0.5.6    # Local storage
```

## 🏗️ Arquitectura MVC con Repository Pattern

```
Presentation Layer (Pages/Widgets - 75 archivos)
    ↓
Controllers (Business Logic - 22 controladores)
    extends ControllerMVC
    ↓
Repositories (Data Access - 11 repositorios)
    API calls + SharedPreferences
    ↓
Models (Data Entities - 26 modelos)
    fromJSON() / toMap()
    ↓
External Services
    ├── HTTP API (REST)
    ├── Firebase (Analytics, FCM)
    ├── Google Maps
    ├── PayPal
    └── SharedPreferences
```

## 📁 Estructura del Proyecto

```
lib/
├── main.dart                          # Entry point con DynamicTheme
├── route_generator.dart               # Navegación con rutas nombradas
├── generated/                         # i18n localization
└── src/
    ├── controllers/      (22 archivos, 1471 líneas)
    │   ├── cart_controller.dart
    │   ├── checkout_controller.dart
    │   ├── food_controller.dart
    │   ├── order_controller.dart
    │   └── user_controller.dart
    ├── models/           (26 archivos)
    │   ├── food.dart, order.dart, user.dart
    │   ├── payment.dart, restaurant.dart
    │   └── cart.dart, address.dart
    ├── pages/            (30 pantallas)
    │   ├── home.dart, cart.dart, checkout.dart
    │   ├── food.dart, orders.dart, tracking.dart
    │   └── login.dart, settings.dart
    ├── elements/         (45 widgets reutilizables)
    │   ├── FoodGridItemWidget
    │   ├── CartItemWidget
    │   └── CreditCardsWidget
    ├── repository/       (11 repositorios)
    │   ├── food_repository.dart
    │   ├── order_repository.dart
    │   └── user_repository.dart
    └── helpers/          (4 archivos)
        ├── configuration.dart
        └── maps_util.dart

assets/
├── cfg/configurations.json    # API base URLs
├── img/                       # Recursos UI
└── fonts/                     # Poppins (9 pesos)
```

## ✨ Características Principales

### 🍔 Descubrimiento de Comida
- Explorar restaurantes por categoría
- Búsqueda de comida y restaurantes
- Comidas en tendencia
- Filtros por categoría
- Detalles de comida con imágenes

### 🛒 Shopping Cart
- Añadir/remover items
- Customización con extras
- Cálculo de subtotales
- Validación de stock
- Persistencia de carrito

### 💳 Checkout & Pagos
- Selección de dirección de entrega
- Métodos de pago múltiples:
  - 💵 Cash on Delivery
  - 💳 Credit/Debit Cards (Visa, Mastercard)
  - 🅿️ PayPal
  - 📱 Digital Wallet
  - 🏪 Pay on Pickup
- Procesamiento seguro
- Confirmación de orden

### 📦 Gestión de Órdenes
- Historial completo
- Tracking en tiempo real
- Estados de orden
- Detalles de entrega
- Generación de invoices

### 👤 Usuario
- Registro y login
- Verificación de teléfono
- Gestión de perfil
- Múltiples direcciones de entrega
- Recuperación de contraseña

### ⭐ Features Adicionales
- Favoritos (comidas favoritas)
- Reviews y ratings
- Notificaciones push (FCM)
- Multi-idioma (9+ idiomas)
- Tema claro/oscuro dinámico
- FAQ y ayuda
- Google Maps para ubicación

## 🔧 Instalación

```bash
# 1. Requisitos
# Flutter SDK 2.x+
# Dart 2.12+
# Android Studio / Xcode

# 2. Clonar
git clone https://github.com/dannyggg3/delivery_client.git
cd delivery_client

# 3. Instalar dependencias
flutter pub get

# 4. Configurar backend
# Editar assets/cfg/configurations.json
{
  "base_url": "https://tubackend.com/api/",
  "apiKey": "TU_API_KEY"
}

# 5. Configurar Firebase
# Agregar google-services.json (Android)
# Agregar GoogleService-Info.plist (iOS)

# 6. Google Maps API
# Agregar key en AndroidManifest.xml y AppDelegate.swift

# 7. Ejecutar
flutter run
```

## 🔌 API Endpoints

| Endpoint | Método | Descripción |
|----------|--------|-------------|
| `/login` | POST | Autenticación de usuario |
| `/register` | POST | Registro de nuevo usuario |
| `/send_reset_link_email` | POST | Reset de contraseña |
| `/foods` | GET | Listado de comidas |
| `/foods/{id}` | GET | Detalles de comida |
| `/categories` | GET | Categorías |
| `/restaurants` | GET | Listado de restaurantes |
| `/favorites` | GET/POST/DELETE | Gestión de favoritos |
| `/orders` | GET/POST | Crear y listar órdenes |
| `/notifications` | GET | Notificaciones de usuario |
| `/settings` | GET | Configuración de app |
| `/payment` | POST | Procesamiento de pagos |

## 💻 Uso

### Configuración Inicial

```dart
// main.dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await GlobalConfiguration().loadFromAsset("configurations");
  runApp(MyApp());
}
```

### Navegación

```dart
Navigator.pushNamed(context, '/Pages', arguments: RouteArgument(id: '1'));
```

### Gestión de Estado

```dart
// Controllers actualizan estado
settingRepo.setting.addListener(() {
  setState(() {}); // UI se actualiza automáticamente
});
```

## 📊 Estadísticas del Proyecto

| Métrica | Valor |
|---------|-------|
| Pantallas | 30 |
| Widgets reutilizables | 45 |
| Modelos | 26 |
| Controllers | 22 (1471 líneas) |
| Repositories | 11 |
| Dependencias | 25+ packages |
| Idiomas soportados | 9+ |
| Platforms | iOS + Android |

## 🔒 Seguridad

- ✅ Autenticación token-based
- ✅ HTTPS para API calls
- ✅ Validación de datos
- ✅ Firebase Authentication
- ✅ Secure storage para credenciales
- ✅ Input sanitization

## 🌐 Internacionalización

```dart
// Cambiar idioma
changeLanguage(Locale locale) {
  settingRepo.setting.value.mobileLanguage.value = locale;
  // UI se actualiza automáticamente
}
```

## 🧪 Testing

```bash
# Unit tests
flutter test

# Integration tests
flutter drive --target=test_driver/app.dart
```

## 🚀 Build & Deploy

```bash
# Android APK
flutter build apk --release

# iOS
flutter build ios --release

# App Bundle (Google Play)
flutter build appbundle --target-platform android-arm,android-arm64,android-x64 --build-number 2 --build-name 1.8.0
```

## 📱 Features por Plataforma

| Feature | Android | iOS |
|---------|---------|-----|
| Push Notifications | ✅ | ✅ |
| Google Maps | ✅ | ✅ |
| Location Services | ✅ | ✅ |
| Deep Links | ✅ | ✅ |
| PayPal | ✅ | ✅ |

## 📈 Mejoras Futuras

- Integración con más pasarelas de pago
- Chat en vivo con restaurante
- Programa de lealtad/puntos
- Compartir en redes sociales
- Pedidos programados
- Órdenes recurrentes
- AR para visualizar comida

## 🛠️ Troubleshooting

| Problema | Solución |
|----------|----------|
| Error de Google Maps | Verificar API key habilitada |
| Push no llegan | Validar google-services.json |
| Crash en iOS | Verificar permissions en Info.plist |
| Error de red | Verificar base_url en configurations.json |

## 📚 Referencias

- [Flutter Documentation](https://flutter.dev/docs)
- [MVC Pattern Package](https://pub.dev/packages/mvc_pattern)
- [Firebase for Flutter](https://firebase.google.com/docs/flutter/setup)
- [Google Maps Flutter](https://pub.dev/packages/google_maps_flutter)

## 📄 Licencia

MIT - Proyecto parte del portafolio de dannyggg3

## 👤 Autor

**dannyggg3** - [@dannyggg3](https://github.com/dannyggg3)

---

⭐ App profesional de food delivery con arquitectura MVC, múltiples métodos de pago y experiencia de usuario optimizada
