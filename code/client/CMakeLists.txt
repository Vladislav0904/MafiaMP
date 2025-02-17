set(MAFIAMP_CLIENT_FILES
        src/main.cpp
        src/core/luavm.cpp
        src/core/application.cpp
        src/core/dev_features.cpp
        src/core/ui/console.cpp
        src/core/ui/chat.cpp
        src/core/states/initialize.cpp
        src/core/states/menu.cpp
        src/core/states/session_connected.cpp
        src/core/states/session_connection.cpp
        src/core/states/session_disconnection.cpp
        src/core/states/session_offline_debug.cpp
        src/core/states/shutdown.cpp
        src/core/hooks/application.cpp
        src/core/hooks/camera.cpp
        src/core/hooks/character_controller.cpp
        src/core/hooks/fast_load.cpp
        src/core/hooks/loading_screen.cpp
        src/core/hooks/mod_init.cpp
        src/core/hooks/render_device.cpp
        src/core/hooks/traffic.cpp
        src/core/hooks/vehicle.cpp
        src/core/hooks/weapon_controller.cpp
        src/core/modules/vehicle.cpp
        src/core/modules/human.cpp
        src/game/module.cpp
        src/game/streaming/entity_factory.cpp
        src/game/helpers/controls.cpp
        src/game/helpers/camera.cpp
        src/game/helpers/human.cpp
        src/game/overrides/character_controller.cpp
        ${CMAKE_BINARY_DIR}/mafiamp_version.cpp
        )

set(MAFIAMP_SDK_FILES
        src/sdk/entities/human/c_human_inventory.cpp
        src/sdk/entities/human/c_human_weapon_controller.cpp
        src/sdk/entities/human/c_human_script.cpp
        src/sdk/entities/player/c_player_model_manager.cpp
        src/sdk/entities/c_car.cpp
        src/sdk/entities/c_door.cpp
        src/sdk/entities/c_entity.cpp
        src/sdk/entities/c_entity_list.cpp
        src/sdk/entities/c_player_2.cpp
        src/sdk/entities/c_vehicle.cpp
        src/sdk/inventory/c_inventory_wrapper.cpp
        src/sdk/mafia/framework/c_mafia_framework.cpp
        src/sdk/mafia/streaming/c_actors_slot_wrapper.cpp
        src/sdk/mafia/streaming/c_slot_wrapper.cpp
        src/sdk/mafia/streaming/c_streaming_module.cpp
        src/sdk/mafia/ui/menu/c_save_menu.cpp
        src/sdk/mafia/ui/navigation/c_navigation.cpp
        src/sdk/mafia/ui/c_game_gui_2_module.cpp
        src/sdk/ue/game/anim/c_wanim_playback_manager.cpp
        src/sdk/ue/game/camera/c_camera.cpp
        src/sdk/ue/game/camera/c_game_camera.cpp
        src/sdk/ue/game/camera/c_cm_player_alternate.cpp
        src/sdk/ue/game/humainai/c_character_controller.cpp
        src/sdk/ue/game/humainai/c_character_state_handler.cpp
        src/sdk/ue/game/human/c_behavior_character.cpp
        src/sdk/ue/game/traffic/c_human_spawner.cpp
        src/sdk/ue/game/traffic/c_profile_spawner.cpp
        src/sdk/ue/gfx/environmenteffects/c_gfx_environment_effects.cpp
        src/sdk/ue/gfx/environmenteffects/c_weather_manager_2.cpp
        src/sdk/ue/sys/core/c_scene_object.cpp
        src/sdk/ue/sys/core/i_core.cpp
        src/sdk/ue/sys/math/c_matrix.cpp
        src/sdk/ue/sys/math/c_quat.cpp
        src/sdk/ue/sys/math/c_vector.cpp
        src/sdk/ue/c_string.cpp
        src/sdk/wrappers/c_human_2_car_wrapper.cpp
        src/sdk/c_game.cpp
        src/sdk/c_game_input_module.cpp
        src/sdk/c_ie.cpp
        src/sdk/c_ticked_module_manager.cpp
        src/sdk/c_time_budget_info.cpp
        src/sdk/patterns.cpp
        )

add_library(MafiaMPClient SHARED ${MAFIAMP_CLIENT_FILES} ${MAFIAMP_SDK_FILES})
target_include_directories(MafiaMPClient PRIVATE src)
target_link_libraries(MafiaMPClient Framework FrameworkClient shlwapi Lua54)
target_link_options(MafiaMPClient PRIVATE /SAFESEH:NO /MANIFEST:NO)

add_custom_command(TARGET MafiaMPClient POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory "${CMAKE_CURRENT_SOURCE_DIR}/../../files" "${CMAKE_BINARY_DIR}/bin/files/"
        )
