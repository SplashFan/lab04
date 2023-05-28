Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в прошлый раз. Настройте сборочные процедуры на различных платформах:

# Task 1
Используйте GitHub Actions для сборки на операционной системе Linux с использованием компиляторов gcc и clang

Копируем репозиторий из предыдущей ЛР:

```
$ git clone https://github.com/SplashFan/lab03_homework lab04
$ cd ~/lab04
$ git remote remove origin
$ git remote add origin https://github.com/SplashFan/lab04
```

И создаем папку со следующим путем: `~/lab04/.github/workflows`
```
$ mkdir .github/workflows
$ cd .github/workflows
```

```
$ cat >> Linux.yml << EOF
name: CMake

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]

jobs: 
 build_Linux:

  runs-on: ubuntu-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build
> EOF

```

```
$ git add Linux.yml
$ git commit -m "Linux.yml - 1"
$ git push origin master
```

# Task 2

Используйте GitHub Actions для сборки на операционной системе Windows

```
$ cat >> Windows.yml << EOF
name: CMake

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]

jobs: 
 build_Windows:

  runs-on: windows-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build
    > EOF
```

```
$ git add Windows.yml
$ git commit -m "Windows.yml - 1"
$ git push origin master
```
