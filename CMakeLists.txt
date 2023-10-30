cmake_minimum_required(VERSION 3.18)
project(lmkd)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_C_STANDARD 17)
set(CMAKE_BUILD_TYPE Release)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++20 -fPIE -Wall -stdlib=libc++ -O3 -flto")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fvisibility=hidden -fforce-emit-vtables")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fvirtual-function-elimination -fwhole-program-vtables")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fintegrated-as --static")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_FILE_OFFSET_BITS=64")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DANDROID_UTILS_REF_BASE_DISABLE_IMPLICIT_CONSTRUCTION")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DLIBLOG_LOG_TAG=1006 -DSNET_EVENT_LOG_TAG=1397638484")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DANDROID_DEBUGGABLE=0")
set(CMAKE_LINK_LIBRARY_FLAG "${CMAKE_LINK_LIBRARY_FLAG} -fuse-ld=lld -static-libstdc++")
set(CMAKE_LINK_LIBRARY_FLAG "${CMAKE_LINK_LIBRARY_FLAG}  -Wl,--icf=all,-O3,--lto-O3,--strip-all")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -fuse-ld=lld -s")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,--icf=all,-O3,--lto-O3,--strip-all --static")

include_directories(
        include/
        libprocessgroup/include/
        libprocessgroup/cgrouprc/include/
        libprocessgroup/cgrouprc_format/include/
        libprocessgroup/setup/include/
        cutils/include/
        cutils/include_outside_system/
        libpsi/include/
        libbase/include/
        liblog/include/
        libutils/include/
        libsystem/include/
        jsoncpp/include/
)
file(GLOB_RECURSE SRCS
        lmkd.cpp
        reaper.cpp
        watchdog.cpp
        liblmkd_utils.cpp
        libpsi/psi.cpp
        libprocessgroup/cgroup_map.cpp
        libprocessgroup/processgroup.cpp
        libprocessgroup/sched_policy.cpp
        libprocessgroup/task_profiles.cpp
        libprocessgroup/cgrouprc/cgroup_controller.cpp
        libprocessgroup/cgrouprc/cgroup_file.cpp
        libprocessgroup/cgrouprc_format/cgroup_controller.cpp
        libprocessgroup/setup/cgroup_map_write.cpp
        cutils/android_get_control_file.cpp
        cutils/android_reboot.cpp
        cutils/config_utils.cpp
        cutils/properties.cpp
        cutils/qtaguid.cpp
        cutils/record_stream.cpp
        cutils/socket_inaddr_any_server_unix.cpp
        cutils/socket_local_client_unix.cpp
        cutils/socket_local_server_unix.cpp
        cutils/sockets.cpp
        cutils/sockets_unix.cpp
        cutils/str_parms.cpp
        cutils/threads.cpp
        libbase/errors_unix.cpp
        libbase/file.cpp
        libbase/hex.cpp
        libbase/logging.cpp
        libbase/parsebool.cpp
        libbase/posix_strerror_r.cpp
        libbase/process.cpp
        libbase/properties.cpp
        libbase/stringprintf.cpp
        libbase/strings.cpp
        libbase/threads.cpp
        liblog/event_tag_map.cpp
        liblog/log_event_list.cpp
        liblog/log_event_write.cpp
        liblog/log_time.cpp
        liblog/logd_reader.cpp
        liblog/logd_writer.cpp
        liblog/logger_name.cpp
        liblog/logger_read.cpp
        liblog/logger_write.cpp
        liblog/logprint.cpp
        liblog/pmsg_reader.cpp
        liblog/pmsg_writer.cpp
        liblog/properties.cpp
        libutils/Errors.cpp
        libutils/FileMap.cpp
        libutils/JenkinsHash.cpp
        libutils/LightRefBase.cpp
        libutils/Looper.cpp
        libutils/NativeHandle.cpp
        libutils/Printer.cpp
        libutils/RefBase.cpp
        libutils/SharedBuffer.cpp
        libutils/StopWatch.cpp
        libutils/String8.cpp
        libutils/String16.cpp
        libutils/StrongPointer.cpp
        libutils/SystemClock.cpp
        libutils/Threads.cpp
        libutils/Timers.cpp
        libutils/Tokenizer.cpp
        libutils/Unicode.cpp
        libutils/VectorImpl.cpp
        jsoncpp/src/lib_json/json_reader.cpp
        jsoncpp/src/lib_json/json_value.cpp
        jsoncpp/src/lib_json/json_writer.cpp
        )
add_executable(lmkd ${SRCS})
