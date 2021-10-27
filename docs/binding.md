### app/build.gradle
```gradle
buildFeatures {
    viewBinding true
}
```

### Gradle -> Sync now

### MainActivity.kt
```kotlin
private lateinit var binding: ActivityMainBinding
onCreate {
    binding = ActivityMainBinding.inflate(layoutInflater)
    setContentView(binding.root)
}
```