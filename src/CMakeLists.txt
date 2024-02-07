target_sources(${EXAWIND_LIB_NAME} PRIVATE
  AMRTiogaIface.cpp
  AMRTiogaIface.h
  AMRWind.cpp
  AMRWind.h
  ExawindSolver.h
  ExawindSolver.cpp
  MPIUtilities.h
  NaluWind.cpp
  NaluWind.h
  OversetSimulation.cpp
  OversetSimulation.h
  ParallelPrinter.h
  MemoryUsage.h
  MemoryUsage.cpp)

target_include_directories(${EXAWIND_LIB_NAME} PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(${EXAWIND_LIB_NAME} PUBLIC
  AMR-Wind::amrwind_api
  AMR-Wind::buildInfoamrwind_obj
  AMReX::amrex
  Nalu-Wind::nalu)

# Solve -fsycl making its way into arguments passed to Kokkos
#if(CMAKE_CXX_COMPILER_ID MATCHES "^(IntelLLVM)$")
#  set(TARGET_FLAGS "")
#  get_target_property(TARGET_FLAGS AMReX::SYCL INTERFACE_COMPILE_OPTIONS)
#  message(STATUS "AMReX options are: ${TARGET_FLAGS}")
#  if((NOT "${TARGET_FLAGS}" STREQUAL "") AND (NOT "${TARGET_FLAGS}" STREQUAL "TARGET_FLAGS-NOTFOUND"))
#    message(STATUS "Removing -fsycl from AMReX options if it exists...")
#    string(REPLACE "-fsycl" "" TARGET_FLAGS ${TARGET_FLAGS})
#    set_target_properties(AMReX::SYCL PROPERTIES INTERFACE_COMPILE_OPTIONS "${TARGET_FLAGS}")
#  endif()
#  set(TARGET_FLAGS "")
#  get_target_property(TARGET_FLAGS AMReX::SYCL INTERFACE_LINK_OPTIONS)
#  message(STATUS "AMReX options are: ${TARGET_FLAGS}")
#  if((NOT "${TARGET_FLAGS}" STREQUAL "") AND (NOT "${TARGET_FLAGS}" STREQUAL "TARGET_FLAGS-NOTFOUND"))
#    message(STATUS "Removing -fsycl from AMReX options if it exists...")
#    string(REPLACE "-fsycl" "" TARGET_FLAGS ${TARGET_FLAGS})
#    set_target_properties(AMReX::SYCL PROPERTIES INTERFACE_LINK_OPTIONS "${TARGET_FLAGS}")
#  endif()
#endif()
