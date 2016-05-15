find_package(Boost 1.44 COMPONENTS date_time filesystem)
include_directories(${Boost_INCLUDE_DIRS})
link_directories   (${Boost_LIBRARY_DIRS})

set(ENV{PKG_CONFIG_PATH} "$ENV{PKG_CONFIG_PATH}:${Caelum_BINARY_DIR}")
find_package(PkgConfig)

# PKG_CHECK_MODULES  (Ogre  OGRE REQUIRED)
# include_directories(${Ogre_INCLUDE_DIRS})
# link_directories   (${Ogre_LIBRARY_DIRS})

PKG_CHECK_MODULES  (OgreOverlay  OGRE-Overlay REQUIRED)
include_directories(${OgreOverlay_INCLUDE_DIRS})
link_directories   (${OgreOverlay_LIBRARY_DIRS})

PKG_CHECK_MODULES  (Ois   OIS  REQUIRED)
include_directories(${Ois_INCLUDE_DIRS})
link_directories   (${Ois_LIBRARY_DIRS})

# PKG_CHECK_MODULES  (Cegui CEGUI-0 REQUIRED)
# include_directories(${Cegui_INCLUDE_DIRS})
# link_directories   (${Cegui_LIBRARY_DIRS})

PKG_CHECK_MODULES  (CeguiOgre CEGUI-0-OGRE REQUIRED)
include_directories(${CeguiOgre_INCLUDE_DIRS})
link_directories   (${CeguiOgre_LIBRARY_DIRS})

# TODO: If Pkgconfig was create correctly, this should work
# PKG_CHECK_MODULES  (Caelum Caelum REQUIRED)
# include_directories(${Caelum_INCLUDE_DIRS})
# link_directories   (${Caelum_LIBRARY_DIRS})
include_directories(${Caelum_SOURCE_DIR}/main/include)
link_directories   (${Caelum_SOURCE_DIR}/lib)
set(Caelum_LIBRARIES -lCaelum)

include_directories(${Caelum_SOURCE_DIR}/samples/include)

add_executable(CaelumLab src/CaelumLab.cpp)
target_link_libraries(CaelumLab
  ${OgreOverlay_LIBRARIES}
  ${Ois_LIBRARIES}
  ${CeguiOgre_LIBRARIES}
  ${Caelum_LIBRARIES}
  ${Boost_LIBRARIES})

add_executable(CaelumDemo src/CaelumDemo.cpp)
target_link_libraries(CaelumDemo
  ${OgreOverlay_LIBRARIES}
  ${Ois_LIBRARIES}
  ${CeguiOgre_LIBRARIES}
  ${Caelum_LIBRARIES}
  ${Boost_LIBRARIES})

# install the executable
INSTALL(TARGETS CaelumLab
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION ${LIB_INSTALL_DIR}
        ARCHIVE DESTINATION ${LIB_INSTALL_DIR}
)

INSTALL(TARGETS CaelumDemo
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION ${LIB_INSTALL_DIR}
        ARCHIVE DESTINATION ${LIB_INSTALL_DIR}
)
