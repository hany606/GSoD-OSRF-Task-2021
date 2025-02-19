cmake_minimum_required(VERSION 3.5)
project(gsod_test_cpp)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(custom_msg_interface REQUIRED)



# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

add_executable(customer src/customer.cpp)
ament_target_dependencies(customer rclcpp std_msgs )

add_executable(customer_msg src/customer_msg.cpp)
ament_target_dependencies(customer_msg rclcpp std_msgs custom_msg_interface)

add_executable(multiplier src/multiplier.cpp)
ament_target_dependencies(multiplier rclcpp std_msgs)

add_executable(multiplier_msg src/multiplier_msg.cpp)
ament_target_dependencies(multiplier_msg rclcpp std_msgs custom_msg_interface)


add_executable(print_test src/print_test.cpp)
target_include_directories(print_test PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)

install(TARGETS 
  print_test
  customer
  multiplier
  customer_msg
  multiplier_msg
  DESTINATION lib/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
