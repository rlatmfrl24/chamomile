---
title: Android Koin-ViewModel-Room 적용해보기
date: '2019-11-17 00:00:11'
draft: false
category: 'Android'
---

## 들어가기 전에

Android 신규 개념 시리즈 첫번째는 내가 개인프로젝트를 시작하면서 적용해가면 배웠던 'Koin-ViewModel-Room' 아키텍쳐이다.

계속해서 공부하다보면, 이 아키텍처도 조잡한 구조의 하나일뿐이지만, 개인적으로는 하나의 개념으로써 공부하는데 꽤 많은 도움이 되서 이렇게 정리해본다.

## 컨셉

프로젝트에 대한 Dependency Injection은 **Koin**으로, View-Model 연결은 *MVVM*패턴을 위한 AAC 중 하나인 **ViewModel**로, 마지막으로 로컬 데이터 관리는 **Room**을 적용했다.

## 프로젝트 구성 절차

### Gradle 구성

```groovy

//ViewModel, Lifecycle, LiveData

implementation 'androidx.appcompat:appcompat:1.1.0'

implementation 'androidx.core:core-ktx:1.1.0'

implementation 'androidx.lifecycle:lifecycle-extensions:2.1.0'

implementation 'androidx.lifecycle:lifecycle-viewmodel-ktx:2.1.0'

implementation 'androidx.lifecycle:lifecycle-livedata-ktx:2.1.0'



//Room

implementation "androidx.room:room-runtime:$room_version"

implementation "androidx.room:room-ktx:$room_version"

kapt "androidx.room:room-compiler:$room_version"



//Koin

implementation "org.koin:koin-core:$koin_version"

implementation "org.koin:koin-android:$koin_version"

implementation "org.koin:koin-androidx-viewmodel:$koin_version"

```

### Room 구성

#### 참조문서: [Android Architecture Components #6 - Room](https://tourspace.tistory.com/28)

Entity-Dao-Database까지 일반적인 구성을 따른다. 이후에 Room Database를 인스턴스화하는 부분은 DI를 위해 **Koin**에서 적용한다.

Koin 적용을 위한 Data Repository를 다음과 같이 구성한다.

`/data/UserRepository.kt`

```kotlin

interface UserRepository {

    fun insert(user: User)

    fun delete()

}

```

해당 인터페이스의 구현부는 다음과 같이 구성한다.

`/data/UserRepositoryImpl.kt`

```kotlin

class UserRepositoryImpl(private val db: FirebaseFirestore, private val userDao: UserDao) : ArticleRepository {

  fun insert(user: User){

    ...

  }

  fun delete(){

    ...

  }

}

```

### Koin 구성

#### 참조문서: [Getting Started with Android ViewModel application](https://start.insert-koin.io/#/quickstart/android-viewmodel)

일반적으로 프로젝트 폴더 내에 'di' 폴더를 만들고 그 안에 구성한다.

`/di/App.kt`

```kotlin

class App : Application(){

    override fun onCreate() {

        super.onCreate()

        startKoin {

            androidLogger()

            androidContext(this@App)

            modules(AppModule)

        }

    }

}

```

AppModule 구성은 다음과 같다.

`/di/AppModule.kt`

```kotlin

val AppModule = module {

//Room Instance

single { Room.databaseBuilder(get(), AppDatabase::class.java, "app_database")

      .fallbackToDestructiveMigration()

      .allowMainThreadQueries()

      .build()

}

//UserRepository DI Component 생성

single { get<AppDatabase>().UserDao() }

single<UserRepository> { UserRepositoryImpl(get(), get()) }

//ViewModel DI 적용

viewModel { MainViewModel(get()) }

}

```

### ViewModel 구성

우선 DI를 받을 ViewModel를 다음과 같이 구성한다.

`/ui/main/MainViewModel.kt`

```kotlin

class MainViewModel(private val user: UserRepository) : ViewModel() {

...

}

```

ViewModel를 구성하고나면 Activity에 다음과 같이 활용할 수 있다.

```kotlin

class MainActivity : AppCompatActivity() {

private val viewModel: MainViewModel by viewModel()

}

```

여기까지 내가 적용해본 Koin-ViewModel-Room Architecture 구조이다. 다음번에는 좀더 진화한 방식으로 구성해 보도록 공부해봐야겠다.
