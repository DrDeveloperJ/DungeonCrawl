cmake_minimum_required(VERSION 3.15)
project(DungeonGame)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(${PROJECT_NAME}
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/main.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Component.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Game.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/GameMediator.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Component.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Player.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Text.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Button.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/PreLoadedElement.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/TextInput.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/UiElement.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/AttackPointsBar.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/PlayerHealthBar.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/ChangeDescriptionButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/ChangeNameButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/CustomizeButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/CustomizeDescriptionButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/CustomizeNameButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/EasyDiffButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/ForwardButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/GuardButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/TreasureButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/UpgradeAttackButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/UpgradeMaxHealthButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/ExploreButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/HardDiffButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/HomePageButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic/RoomSelector.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic/TreasureRoom.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic/EmptyRoom.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic/MonsterRoom.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic/UpgradeRoom.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic/DungeonExploredDisplay.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic/DungeonRoom.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/BackButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/TreasureButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/ForwardButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/MeditateButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/AttackButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/GuardButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/UpgradeAttackButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/Buttons/UpgradeMaxHealthButton.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables/EnemyHealthBar.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/EnemyLogic/CombatMediator.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/EnemyLogic/MovesDisplay.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/EnemyLogic/Enemy.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/EnemyLogic/Goblin.cpp
  ${CMAKE_SOURCE_DIR}/OOPModuleProject/DungeonBackground/DungeonBackgroundCache.cpp
)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_directory
    "${CMAKE_SOURCE_DIR}/OOPModuleProject/Assets"
    "$<TARGET_FILE_DIR:${PROJECT_NAME}>/Assets"
)

target_compile_definitions(${PROJECT_NAME} PRIVATE
    UNICODE
    _UNICODE
    WIN32
    SFML_STATIC
    $<$<CONFIG:Debug>:_DEBUG>
    $<$<CONFIG:Debug>:_CONSOLE>
    $<$<CONFIG:Release>:NDEBUG>
    $<$<CONFIG:Release>:_CONSOLE>
)

target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/dependencies/SFML/include")
target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/OOPModuleProject/Assets")
target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/OOPModuleProject/DungeonBackground")
target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/OOPModuleProject/EnemyLogic")
target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/OOPModuleProject/Reuseables")
target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/OOPModuleProject/RoomLogic")

target_link_directories(${PROJECT_NAME} PUBLIC
    "${CMAKE_SOURCE_DIR}/dependencies/SFML/lib"
)

target_link_libraries(${PROJECT_NAME} PUBLIC
  $<$<CONFIG:Debug>:sfml-graphics-s-d sfml-window-s-d sfml-system-s-d sfml-audio-s-d sfml-network-s-d sfml-main-s-d opengl32 freetype winmm gdi32 flac vorbisenc vorbisfile vorbis ogg ws2_32>
  $<$<OR:$<CONFIG:Release>,$<CONFIG:RelWithDebInfo>>:sfml-graphics-s sfml-window-s sfml-system-s sfml-audio-s sfml-network-s opengl32 freetype winmm gdi32 flac vorbisenc vorbisfile vorbis ogg ws2_32>
)


if(MSVC)
    set_target_properties(${PROJECT_NAME} PROPERTIES
        LINK_FLAGS "/SUBSYSTEM:CONSOLE"
    )
endif()

configure_file(
  "${CMAKE_SOURCE_DIR}/OOPModuleProject/JdmgtR34raz9.ttf"
  "${CMAKE_BINARY_DIR}/JdmgtR34raz9.ttf"
  COPYONLY
)

file(COPY "${CMAKE_SOURCE_DIR}/OOPModuleProject/Assets" DESTINATION "${CMAKE_BINARY_DIR}/Assets")

if(MSVC)
  target_compile_options(${PROJECT_NAME} PRIVATE
    $<$<CONFIG:Debug>:/MDd>
    $<$<CONFIG:Release>:/MD>
  )
endif()