# Apachiy Desktop

Apachiy Desktop is a self-hosted fork of Nuvio Desktop. Cloud accounts, library,
devices, and addons talk to **your** Apachiy backend (`supabase.apachiy.org` /
`api.apachiy.org`), never to Nuvio official infra.

The Kotlin package stays `com.nuvio.app`. Desktop packages ship as **Apachiy**
(`com.apachiy.desktop` on macOS).

## Run from source (Windows)

1. Open the **ApachiyDesktop** folder in your IDE or terminal.
2. Copy `local.example.properties` to `local.properties` (gitignored) and fill in:
   - `APACHIY_SUPABASE_URL`
   - `APACHIY_SUPABASE_ANON_KEY`
   - `APACHIY_API_BASE_URL`
   - the same TMDB / Trakt / Simkl keys you use on Apachiy Mobile and TV
3. Leave `NUVIO_SUPABASE_FALLBACK_URL` empty.
4. Ensure JDK 17+ and the Windows desktop player toolchain (MSVC, WebView2, bundled `libmpv-2.dll`).
5. Run:

```powershell
.\gradlew.bat :composeApp:run
```

Gradle dev runs expose operator settings (addons / content discovery) via
`AppUpdaterPlatform.isDebugBuild`. Packaged MSI/DMG builds hide those sections.

## Cloud

Production Apachiy endpoints:

- Supabase: `https://supabase.apachiy.org`
- API: `https://api.apachiy.org`
- Dashboard / devices: `https://apachiy.org/dashboard`

Do not copy Coolify, Kong, Traefik, Studio, `infra/supabase/`, or SQL migrations
into this repo. Those live in the cloud / TV / API stacks.

## Tests

```powershell
.\gradlew.bat :composeApp:compileKotlinDesktop
.\gradlew.bat :composeApp:desktopTest
```
