## Changelog for plugins (1.0.1)

1. Dependency:

Instead of using the outdated `core-parsers` lib, `core-parsers` and `core-exts` have now been merged into **Tsuki**, a unified library for both Usagi and its plugins.
We will adopt it as the standard convention for future plugins.

```diff
- core = "9b51187e96"
+ tsuki = "1.0.2"
kotlin = "2.2.10"
ksp = "2.2.10-2.0.2"
coroutines = "1.10.2"

[libraries]
- core-parsers = { module = "com.github.UsagiApp:core-parsers", version.ref = "core"}
+ tsuki = { module = "com.github.UsagiApp:Tsuki", version.ref = "tsuki"}
```

In `build.gradle.kts`:

```diff
- api(libs.core.parsers)
+ api(libs.tsuki)
```

2. Parser processor:

Use `plugins-ksp` folder in plugin template project to build `MangaSource` and some core files according to the new module structure standard, excluding classes belonging to Tachiyomi (stub).

3. Sources:

- Move the entire **`org.koitharu.kotatsu.parsers.*`** module to **`tsuki.*`**, for example:

```diff
- import org.koitharu.kotatsu.parsers.ErrorMessages
- import org.koitharu.kotatsu.parsers.MangaLoaderContext
- import org.koitharu.kotatsu.parsers.MangaSourceParser
- import org.koitharu.kotatsu.parsers.bitmap.Bitmap
- import org.koitharu.kotatsu.parsers.bitmap.Rect
- import org.koitharu.kotatsu.parsers.config.ConfigKey
- import org.koitharu.kotatsu.parsers.core.PagedMangaParser
- import org.koitharu.kotatsu.parsers.model.*
- import org.koitharu.kotatsu.parsers.network.CloudFlareHelper
- import org.koitharu.kotatsu.parsers.network.UserAgents
- import org.koitharu.kotatsu.parsers.util.*
- import org.koitharu.kotatsu.parsers.util.json.*
+ import tsuki.ErrorMessages
+ import tsuki.MangaLoaderContext
+ import tsuki.MangaSourceParser
+ import tsuki.bitmap.Bitmap
+ import tsuki.bitmap.Rect
+ import tsuki.config.ConfigKey
+ import tsuki.core.PagedMangaParser
+ import tsuki.model.*
+ import tsuki.network.CloudFlareHelper
+ import tsuki.network.UserAgents
+ import tsuki.util.*
+ import tsuki.util.json.*
```

- It's not necessary to declare `filter.query` or `filter.author` using `val` variables; they can be called directly from API (and may be null, empty or blank):

```diff
// Old method
- val query = filter.query
val url = buildString {
-  if (!query.isNullOrEmpty() || filter.tags.isNotEmpty() || filter.states.isNotEmpty()) {
// Current method
+  if (!filter.query.isNullOrEmpty() || filter.tags.isNotEmpty() || filter.states.isNotEmpty()) {

// Old method
if (!filter.query.isNullOrEmpty()) {
  append("&filter[name]=")
-  append(filter.query?.urlEncoded() ?: "")
// Current method
+  append(filter.query.urlEncoded())

// Old method
- append(filter.author!!.urlEncoded())
// Current method
+ append(filter.author.urlEncoded())
```

- Remember to remove all Tachiyomi sources and its compatibility layer in your plugin project, it will not work (the entire stub layer has been removed in favor of native external sources).

4. Build:

Continue using `buildJar` task provided in plugin template project to build all sources and some core files into a complete plugin in .JAR format.

## Changelog for plugins (1.0.2)

### Dependencies:

In `libs.versions.toml`:

- Upgrade `tsuki` to 1.0.3, `serialization` to 1.11.0

## Changelog for plugins (1.0.3)

### Dependencies:

In `libs.versions.toml`:

- Upgrade `tsuki` to 1.0.5
