add_library(catch_main STATIC catch_main.cpp)
target_link_libraries(catch_main PUBLIC Catch2::Catch2)

add_library(testing)
target_link_libraries(testing PUBLIC catch_main glpp::gl glpp::core glpp::system)
add_library(glpp::testing ALIAS testing)

set(glpp-test-files
    ${CMAKE_CURRENT_LIST_DIR}/src/context.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/offscreen_driver.cpp
)
target_sources(testing PRIVATE ${glpp-test-files})
target_include_directories(testing PUBLIC
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)