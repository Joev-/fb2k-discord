add_library(foobar2000_shared STATIC IMPORTED GLOBAL)
set_target_properties(foobar2000_shared PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/shared-Win32.lib)
