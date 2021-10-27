---
layout: default
title: Navigation
parent: Jetpack Compose
nav_order: 1
---

### MainActivity.kt

```kotlin
import androidx.navigation.NavHostController
import androidx.navigation.compose.rememberNavController

class MainActivity : ComponentActivity() {

    private lateinit var navController: NavHostController

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            DogSearchTheme {
                navController = rememberNavController()
                SetupNavGraph(navController = navController)
            }
        }
    }
}
```
### Screen.kt

```kotlin
sealed class Screen(val route: String) {
    object BreedsList : Screen(route = "breeds_list_screen")
    object DogImage : Screen(route = "dog_image_screen")
}
```


### NavGraph.kt

```kotlin
import androidx.compose.runtime.Composable
import androidx.navigation.NavHostController
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable

@Composable
fun SetupNavGraph(
    navController: NavHostController
) {
    NavHost(
        navController = navController,
        startDestination = Screen.BreedsList.route
    ) {
        composable(
            route = Screen.BreedsList.route
        ) {
            val viewModel = DogBreedsListModel()
            BreedsListScreen(navController = navController, viewModel = viewModel)
        }
        composable(
            route = Screen.DogImage.route + "/{breedName}"
        ) { navBackStack ->
            val breedName = navBackStack.arguments?.getString("breedName")

            val viewModel = BreedImageModel(breedName = breedName)
            DogImageScreen(viewModel)
        }
    }
}
```

### BreedsListScreen.kt
```kotlin
fun BreedsListScreen(
    navController: NavController,
    viewModel: DogBreedsListModel = DogBreedsListModel()
) {
    OutlinedButton(
        onClick = {
            navigate(
                navController = navController,
                breedName = breedName,
                subBreedName = ""
            )
        }
    ) { 
        Text(text = "Image")
    }
}
```

