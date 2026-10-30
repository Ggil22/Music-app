# Muflix – Aplicación de Música

**Muflix** es una aplicación de streaming de música en Java, desarrollada en grupo para la asignatura **Proyecto de Análisis y Diseño de Software (PADSOF)** de la Universidad Autónoma de Madrid.

Permite a los usuarios subir, reproducir y organizar canciones en álbumes y listas de reproducción, con un sistema de usuarios premium, seguidores y moderación de contenido por parte de un administrador.

## Funcionalidades

### Usuarios
- **Anónimo**: puede registrarse, iniciar sesión y reproducir un número limitado de canciones.
- **Miembro registrado**:
  - Subir canciones (MP3) y crear **álbumes** y **playlists**.
  - Reproducir canciones, álbumes y playlists (con reproducción automática opcional).
  - **Seguir** a otros usuarios y consultar su actividad.
  - **Denunciar plagios** de canciones.
  - Hacerse **premium** pagando con tarjeta, lo que elimina el límite de reproducciones.
  - Las canciones con contenido explícito solo pueden reproducirlas los mayores de edad.
- **Administrador**:
  - Validar las canciones subidas y marcarlas como explícitas o no.
  - Aceptar o rechazar denuncias de plagio.
  - Bloquear, desbloquear, banear y desbanear miembros.
  - Configurar los parámetros del sistema.

### Configuración (`Muflix/config/config.txt`)

| Parámetro | Descripción | Valor por defecto |
|-----------|-------------|:-----------------:|
| `maxReproducciones` | Reproducciones permitidas para usuarios no premium | 10 |
| `numRepsPremium` | Reproducciones necesarias para obtener premium gratis (parámetro definido, aún no aplicado en la lógica) | 20 |
| `periodoPremium` | Duración del premium (días) | 30 |
| `diasBloqueoTemporal` | Duración del bloqueo temporal de un miembro (días) | 3 |
| `precioPremium` | Precio del premium (€) | 15.0 |

## Estructura

```
Muflix/
├── src/com/padsof/muflix/
│   ├── core/          # Clase principal Muflix (singleton): datos, carga y guardado
│   ├── usuario/       # Usuario, Anonimo, Registrado, Miembro, Administrador
│   ├── media/         # ElementoMultimedia, Cancion, Album, Playlist
│   ├── denuncia/      # Denuncias de plagio
│   ├── exceptions/    # Excepciones propias (usuario baneado, contraseña incorrecta…)
│   ├── utils/         # Constantes, fechas simuladas y funciones auxiliares
│   └── testers/       # Tests JUnit y programa de prueba (Tester01)
├── data/              # "Base de datos" en ficheros de texto y canciones MP3 de ejemplo
├── config/            # Fichero de configuración
└── lib/               # Librerías externas
```

Los datos se guardan en ficheros de texto con campos separados por `|` (`db_miembros.txt`, `db_canciones.txt`, `db_albumes.txt`, `db_playlists.txt`, `db_follows.txt`, `db_denuncias.txt`).

## Tecnologías

- **Java**
- **JUnit 4** para las pruebas
- Librerías externas (`Muflix/lib/`):
  - `MP3Player.jar` y `jl1.0.1.jar` (JLayer): reproducción de MP3.
  - `TeleChargeAndPaySystem8.jar`: simulación de pagos con tarjeta.

## Cómo ejecutarlo

El proyecto está pensado para importarse en **Eclipse** (u otro IDE Java):

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/Ggil22/Music-app.git
   ```
2. Importar la carpeta `Muflix` como proyecto Java.
3. Añadir los `.jar` de `Muflix/lib/` y JUnit 4 al *build path*.
4. Usar `Muflix/` como directorio de trabajo, ya que las rutas a `data/` y `config/` son relativas.
5. Ejecutar `com.padsof.muflix.testers.Tester01` (demo con reproducción de una playlist) o la suite de tests `AllTesters`.

Desde la línea de comandos (Linux/macOS; en Windows usa `;` en lugar de `:` en el classpath):

```bash
cd Muflix
javac -d bin -cp "lib/*:/ruta/a/junit-4.jar:/ruta/a/hamcrest-core.jar" $(find src -name "*.java")
java -cp "bin:lib/*" com.padsof.muflix.testers.Tester01
```

## Autores

Grupo 4 – PADSOF 2261, Universidad Autónoma de Madrid. Incluye a **Guillermo Gil Ochoa** — [GitHub](https://github.com/Ggil22)
