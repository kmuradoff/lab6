cmake_minimum_required(VERSION 2.8) #Проверка версии CMake.

set(PROJECT_NAME LAB_6) #Создаем обычную локальную переменную с именем проекта
project(${PROJECT_NAME}) # Название проекта

#Переменная с именем библиотеки
set(main main)
set(StackLib StackLib)
set(PolishLib PolishLib)

set(CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING "Configs" FORCE) #Создается переменная CMAKE_CONFIGURATION_TYPES со значением "Debug;Release" и меткой/разделом Configs, переменная сохраниется в специальном файле доступном из всех файлов,
if(NOT CMAKE_BUILD_TYPE) # проверка имеющихся у компилятора вариантов сборки
  set(CMAKE_BUILD_TYPE Release) #Если нет то устанавливаем Release
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE})

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/StackLib 
${CMAKE_CURRENT_SOURCE_DIR}/PolishLib) 

#Добавляем директорию с под-CMakeList-ом, и выполняем под-CMakeList
add_subdirectory(main)
add_subdirectory(StackLib)
add_subdirectory(PolishLib)

add_subdirectory(gtest)
add_subdirectory(test)