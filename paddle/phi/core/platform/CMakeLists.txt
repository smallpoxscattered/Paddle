set(DEVICE_SRCS "")

list(APPEND DEVICE_SRCS collective_helper.cc profiler.cc)

if(WITH_GPU OR WITH_ROCM)
  list(APPEND DEVICE_SRCS device/gpu/gpu_info.cc profiler.cu
       device/gpu/gpu_resource_pool.cc)
endif()

if(WITH_XPU)
  list(APPEND DEVICE_SRCS device/xpu/xpu_info.cc
       device/xpu/xpu_resource_pool.cc)
endif()

if(WITH_CUSTOM_DEVICE)
  list(APPEND DEVICE_SRCS device/custom/custom_device_resource_pool.cc)
endif()

# device event library
list(APPEND DEVICE_SRCS device_event_base.cc)
if(WITH_GPU OR WITH_ROCM)
  list(APPEND DEVICE_SRCS device_event_gpu.cc)
endif()
if(WITH_CUSTOM_DEVICE)
  list(APPEND DEVICE_SRCS device_event_custom_device.cc)
endif()

list(APPEND DEVICE_SRCS cuda_graph_with_memory_pool.cc)
list(APPEND DEVICE_SRCS device_context.cc gen_comm_id_helper.cc)
collect_srcs(core_srcs SRCS ${DEVICE_SRCS})
