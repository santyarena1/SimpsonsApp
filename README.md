2do Parcial - Parte Practica

Fork del repo original https://github.com/ExBattou/SimpsonsApp

Alumno: Santiago Arena

Abrí un issue por cada error encontrado, en cada uno está el archivo, la linea y como lo resolvería. No toqué nada del codigo, solo este readme.

Errores encontrados:

1 - Episode.kt, lineas 13 a 16. Hay un bloque init colgado afuera de la clase con un return que no compila.
Solucion: borrar las lineas 13 a 16, dejar solo el data class.

2 - MainActivity.kt linea 17. Usa MaterialTheme directo en vez del SimpsonsAppTheme que esta definido en theme/Theme.kt, asi nunca se aplica el theme custom.
Solucion: importar SimpsonsAppTheme y reemplazar MaterialTheme { ... } por SimpsonsAppTheme { ... }.

3 - MainScreen.kt lineas 44 y 45 y DetailScreen.kt linea 32. Usan collectAsState en vez de collectAsStateWithLifecycle, no respeta el ciclo de vida.
Solucion: importar androidx.lifecycle.compose.collectAsStateWithLifecycle y reemplazar las tres llamadas a collectAsState() por collectAsStateWithLifecycle().

4 - MainScreen.kt lineas 51 a 53. La llamada a refreshSeasons() esta en el cuerpo del composable, se ejecuta en cada recomposicion.
Solucion: envolver el if en un LaunchedEffect(episodes.loadState.refresh, seasons) { ... }.

5 - MainScreen.kt linea 119. La lista esta hecha con LazyRow y deberia ser LazyColumn, las cards son verticales.
Solucion: cambiar LazyRow por LazyColumn.

6 - EpisodeRepository.kt linea 8. Esta declarada como get_episodes() en snake_case y el override del Impl la llama getEpisodes(), no matchea y no compila.
Solucion: renombrar la funcion en la interface a getEpisodes() y actualizar la llamada en GetEpisodesUseCase.kt linea 13.

7 - EpisodeRepositoryImpl.kt linea 18. Falta el import de SimpsonsApi.
Solucion: agregar import com.example.simpsonsapp.data.remote.SimpsonsApi.

8 - DataModule.kt lineas 34 a 37. Al Retrofit.Builder() le falta el .baseUrl(), apenas se construye tira IllegalStateException.
Solucion: agregar .baseUrl("https://thesimpsonsapi.com/api/") antes de .build(). Aprovechar y cambiar en EpisodeRemoteMediator.kt linea 106 el @GET("https://...") por @GET("episodes").

9 - MainScreenViewModel.kt y DataRepository.kt. Quedaron del template, no usan Hilt, el repository no esta provisto en el modulo de DI y ninguna pantalla los usa.
Solucion: eliminar MainScreenViewModel.kt, DataRepository.kt y el test MainScreenViewModelTest.kt.

10 - AppNavigation.kt lineas 9 y 10. Tiene dos imports wildcard que no aportan nada (androidx.navigation.* y androidx.compose.*).
Solucion: borrar las lineas 9 y 10.

Issues: https://github.com/santyarena1/SimpsonsApp/issues
