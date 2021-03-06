find_package (Qt5 REQUIRED COMPONENTS
    Core
    Gui
)

find_package (KF5 REQUIRED COMPONENTS
    Config
    CoreAddons
    WindowSystem
)

find_package (KWinEffects REQUIRED)

set (effect_SRCS
    plugin.cc
    Disappear3Effect.cc
)

kconfig_add_kcfg_files (effect_SRCS
    disappear3config.kcfgc
)

add_library (kwin4_effect_disappear3 SHARED ${effect_SRCS})

target_link_libraries (kwin4_effect_disappear3
    PUBLIC
        Qt5::Core
        Qt5::Gui
        KF5::ConfigCore
        KF5::ConfigGui
        KF5::CoreAddons
        KF5::WindowSystem
        KWinEffects::KWinEffects
)

kcoreaddons_desktop_to_json (kwin4_effect_disappear3 disappear3.desktop
    SERVICE_TYPES kwineffect.desktop
)

install (
    TARGETS
        kwin4_effect_disappear3

    DESTINATION
        ${PLUGIN_INSTALL_DIR}/kwin/effects/plugins/
)
