# Lab03
В рамках выполнения данной лабораторной работы мною были выполнены все команды из tutorial:
1) Скопирован репозиторий из lab02:
```bash
git clone https://github.com/${GITHUB_USERNAME}/lab02.git projects/lab03
Клонирование в «projects/lab03»...
remote: Enumerating objects: 19, done.
remote: Counting objects: 100% (19/19), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 19 (delta 2), reused 12 (delta 0), pack-reused 0 (from 0)
Получение объектов: 100% (19/19), готово.
Определение изменений: 100% (2/2), готово.
$ cd projects/lab03
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git
```
2) Выполнена ручная компиляция:
```bash
$ g++ -std=c++11 -I./include -c sources/print.cpp
$ nm print.o | grep print
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
0000000000000026 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
```
```bash
$ ar rvs print.a print.o
ar: создаётся print.a
a - print.o
```
```bash
$ g++ -std=c++11 -I./include -c examples/example1.cpp
$ g++ example1.o print.a -o example1
$ ./example1 && echo
hello
```
```bash
$ g++ -std=c++11 -I./include -c examples/example2.cpp
$ nm example2.o
0000000000000000 V DW.ref.__gxx_personality_v0
                 U __gxx_personality_v0
0000000000000000 T main
                 U _Unwind_Resume
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED2Ev
0000000000000000 n _ZNSt15__new_allocatorIcED5Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct


$ ./example2
cat log.txt && echo
hello
```
3) Создан CMakeLists.txt:
```bash
$ cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)
project(print)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

add_executable(example1 ${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 ${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
target_link_libraries(example1 print)
target_link_libraries(example2 print)
```
4) Произведена автоматическая сборка проекта и протестированы функции файлов examples:
```bash
cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
ksu@skalab3:~/shirmanovak410-ops/workspace/projects/lab03$ cmake --build _build --target example1
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[100%] Linking CXX executable example1
[100%] Built target example1
ksu@skalab3:~/shirmanovak410-ops/workspace/projects/lab03$ cmake --build _build --target example2
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[100%] Linking CXX executable example2
[100%] Built target example2
```
5) Скопирован CMakeLists.txt из репозитория лабы и выполнена сборка с его помощью:
```bash
$ cmake --build _build --target install
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/lib/libprint.a
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/include
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/include/print.hpp
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/cmake/print-config.cmake
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/cmake/print-config-noconfig.cmake

$ tree _install
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

4 directories, 4 files
```
6) Этот CMakeLists.txt закоммичен на данный репозиторий


