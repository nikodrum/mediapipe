workspace(name = "mediapipe")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "bazel_skylib",
    type = "tar.gz",
    urls = [
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.0.3/bazel-skylib-1.0.3.tar.gz",
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.0.3/bazel-skylib-1.0.3.tar.gz",
    ],
    sha256 = "1c531376ac7e5a180e0237938a2536de0c54d93f5c278634818e0efc952dd56c",
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()
load("@bazel_skylib//lib:versions.bzl", "versions")
versions.check(minimum_bazel_version = "3.7.2")

# ABSL cpp library lts_2021_03_24, patch 2.
http_archive(
    name = "com_google_absl",
    urls = [
        "https://github.com/abseil/abseil-cpp/archive/refs/tags/20210324.2.tar.gz",
    ],
    # Remove after https://github.com/abseil/abseil-cpp/issues/326 is solved.
    patches = [
        "@//third_party:com_google_absl_f863b622fe13612433fdf43f76547d5edda0c93001.diff"
    ],
    patch_args = [
        "-p1",
    ],
    strip_prefix = "abseil-cpp-20210324.2",
    sha256 = "59b862f50e710277f8ede96f083a5bb8d7c9595376146838b9580be90374ee1f"
)

http_archive(
    name = "rules_cc",
    strip_prefix = "rules_cc-main",
    urls = ["https://github.com/bazelbuild/rules_cc/archive/main.zip"],
)

http_archive(
   name = "rules_foreign_cc",
   strip_prefix = "rules_foreign_cc-0.1.0",
   url = "https://github.com/bazelbuild/rules_foreign_cc/archive/0.1.0.zip",
)

load("@rules_foreign_cc//:workspace_definitions.bzl", "rules_foreign_cc_dependencies")

rules_foreign_cc_dependencies()

# This is used to select all contents of the archives for CMake-based packages to give CMake access to them.
all_content = """filegroup(name = "all", srcs = glob(["**"]), visibility = ["//visibility:public"])"""

# GoogleTest/GoogleMock framework. Used by most unit-tests.
# Last updated 2021-07-02.
http_archive(
    name = "com_google_googletest",
    urls = ["https://github.com/google/googletest/archive/4ec4cd23f486bf70efcc5d2caa40f24368f752e3.zip"],
    strip_prefix = "googletest-4ec4cd23f486bf70efcc5d2caa40f24368f752e3",
    sha256 = "de682ea824bfffba05b4e33b67431c247397d6175962534305136aa06f92e049",
)

# Google Benchmark library v1.6.1 released on 2022-01-10.
http_archive(
    name = "com_google_benchmark",
    urls = ["https://github.com/google/benchmark/archive/refs/tags/v1.6.1.tar.gz"],
    strip_prefix = "benchmark-1.6.1",
    sha256 = "6132883bc8c9b0df5375b16ab520fac1a85dc9e4cf5be59480448ece74b278d4",
    build_file = "@//third_party:benchmark.BUILD",
)

# gflags needed by glog
http_archive(
    name = "com_github_gflags_gflags",
    strip_prefix = "gflags-2.2.2",
    sha256 = "19713a36c9f32b33df59d1c79b4958434cb005b5b47dc5400a7a4b078111d9b5",
    url = "https://github.com/gflags/gflags/archive/v2.2.2.zip",
)

# 2020-08-21
http_archive(
    name = "com_github_glog_glog",
    strip_prefix = "glog-0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6",
    sha256 = "58c9b3b6aaa4dd8b836c0fd8f65d0f941441fb95e27212c5eeb9979cfd3592ab",
    urls = [
        "https://github.com/google/glog/archive/0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6.zip",
    ],
)
http_archive(
    name = "com_github_glog_glog_no_gflags",
    strip_prefix = "glog-0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6",
    sha256 = "58c9b3b6aaa4dd8b836c0fd8f65d0f941441fb95e27212c5eeb9979cfd3592ab",
    build_file = "@//third_party:glog_no_gflags.BUILD",
    urls = [
        "https://github.com/google/glog/archive/0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6.zip",
    ],
    patches = [
        "@//third_party:com_github_glog_glog_9779e5ea6ef59562b030248947f787d1256132ae.diff",
    ],
    patch_args = [
        "-p1",
    ],
)

# easyexif
http_archive(
    name = "easyexif",
    url = "https://github.com/mayanklahiri/easyexif/archive/master.zip",
    strip_prefix = "easyexif-master",
    build_file = "@//third_party:easyexif.BUILD",
)

# libyuv
http_archive(
    name = "libyuv",
    # Error: operand type mismatch for `vbroadcastss' caused by commit 8a13626e42f7fdcf3a6acbb0316760ee54cda7d8.
    urls = ["https://chromium.googlesource.com/libyuv/libyuv/+archive/2525698acba9bf9b701ba6b4d9584291a1f62257.tar.gz"],
    build_file = "@//third_party:libyuv.BUILD",
)

# Note: protobuf-javalite is no longer released as a separate download, it's included in the main Java download.
# ...but the Java download is currently broken, so we use the "source" download.
http_archive(
    name = "com_google_protobuf_javalite",
    sha256 = "87407cd28e7a9c95d9f61a098a53cf031109d451a7763e7dd1253abf8b4df422",
    strip_prefix = "protobuf-3.19.1",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.19.1.tar.gz"],
)

http_archive(
    name = "com_google_protobuf",
    sha256 = "87407cd28e7a9c95d9f61a098a53cf031109d451a7763e7dd1253abf8b4df422",
    strip_prefix = "protobuf-3.19.1",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.19.1.tar.gz"],
    patches = [
        "@//third_party:com_google_protobuf_fixes.diff"
    ],
    patch_args = [
        "-p1",
    ],
)

http_archive(
    name = "com_google_audio_tools",
    strip_prefix = "multichannel-audio-tools-master",
    urls = ["https://github.com/google/multichannel-audio-tools/archive/master.zip"],
)

# 2020-07-09
http_archive(
    name = "pybind11_bazel",
    strip_prefix = "pybind11_bazel-203508e14aab7309892a1c5f7dd05debda22d9a5",
    urls = ["https://github.com/pybind/pybind11_bazel/archive/203508e14aab7309892a1c5f7dd05debda22d9a5.zip"],
    sha256 = "75922da3a1bdb417d820398eb03d4e9bd067c4905a4246d35a44c01d62154d91",
)

# Point to the commit that deprecates the usage of Eigen::MappedSparseMatrix.
http_archive(
    name = "pybind11",
    urls = [
        "https://github.com/pybind/pybind11/archive/70a58c577eaf067748c2ec31bfd0b0a614cffba6.zip",
    ],
    sha256 = "b971842fab1b5b8f3815a2302331782b7d137fef0e06502422bc4bc360f4956c",
    strip_prefix = "pybind11-70a58c577eaf067748c2ec31bfd0b0a614cffba6",
    build_file = "@pybind11_bazel//:pybind11.BUILD",
)

# Point to the commit that deprecates the usage of Eigen::MappedSparseMatrix.
http_archive(
    name = "ceres_solver",
    url = "https://github.com/ceres-solver/ceres-solver/archive/123fba61cf2611a3c8bddc9d91416db26b10b558.zip",
    patches = [
        "@//third_party:ceres_solver_compatibility_fixes.diff"
    ],
    patch_args = [
        "-p1",
    ],
    strip_prefix = "ceres-solver-123fba61cf2611a3c8bddc9d91416db26b10b558",
    sha256 = "8b7b16ceb363420e0fd499576daf73fa338adb0b1449f58bea7862766baa1ac7"
)

http_archive(
    name = "opencv",
    build_file_content = all_content,
    strip_prefix = "opencv-3.4.10",
    urls = ["https://github.com/opencv/opencv/archive/3.4.10.tar.gz"],
)

new_local_repository(
    name = "linux_opencv",
    build_file = "@//third_party:opencv_linux.BUILD",
    path = "/usr",
)

new_local_repository(
    name = "linux_ffmpeg",
    build_file = "@//third_party:ffmpeg_linux.BUILD",
    path = "/usr"
)

new_local_repository(
    name = "macos_opencv",
    build_file = "@//third_party:opencv_macos.BUILD",
    # For local MacOS builds, the path should point to an opencv@3 installation.
    # If you edit the path here, you will also need to update the corresponding
    # prefix in "opencv_macos.BUILD".
    path = "/usr/local",
)

new_local_repository(
    name = "macos_ffmpeg",
    build_file = "@//third_party:ffmpeg_macos.BUILD",
    path = "/usr/local/opt/ffmpeg",
)

new_local_repository(
    name = "windows_opencv",
    build_file = "@//third_party:opencv_windows.BUILD",
    path = "C:\\opencv\\build",
)

http_archive(
    name = "android_opencv",
    build_file = "@//third_party:opencv_android.BUILD",
    strip_prefix = "OpenCV-android-sdk",
    type = "zip",
    url = "https://github.com/opencv/opencv/releases/download/3.4.3/opencv-3.4.3-android-sdk.zip",
)

# After OpenCV 3.2.0, the pre-compiled opencv2.framework has google protobuf symbols, which will
# trigger duplicate symbol errors in the linking stage of building a mediapipe ios app.
# To get a higher version of OpenCV for iOS, opencv2.framework needs to be built from source with
# '-DBUILD_PROTOBUF=OFF -DBUILD_opencv_dnn=OFF'.
http_archive(
    name = "ios_opencv",
    sha256 = "7dd536d06f59e6e1156b546bd581523d8df92ce83440002885ec5abc06558de2",
    build_file = "@//third_party:opencv_ios.BUILD",
    type = "zip",
    url = "https://github.com/opencv/opencv/releases/download/3.2.0/opencv-3.2.0-ios-framework.zip",
)

http_archive(
    name = "stblib",
    strip_prefix = "stb-b42009b3b9d4ca35bc703f5310eedc74f584be58",
    sha256 = "13a99ad430e930907f5611325ec384168a958bf7610e63e60e2fd8e7b7379610",
    urls = ["https://github.com/nothings/stb/archive/b42009b3b9d4ca35bc703f5310eedc74f584be58.tar.gz"],
    build_file = "@//third_party:stblib.BUILD",
    patches = [
        "@//third_party:stb_image_impl.diff"
    ],
    patch_args = [
        "-p1",
    ],
)

# Needed by TensorFlow
http_archive(
    name = "io_bazel_rules_closure",
    sha256 = "e0a111000aeed2051f29fcc7a3f83be3ad8c6c93c186e64beb1ad313f0c7f9f9",
    strip_prefix = "rules_closure-cf1e44edb908e9616030cc83d085989b8e6cd6df",
    urls = [
        "http://mirror.tensorflow.org/github.com/bazelbuild/rules_closure/archive/cf1e44edb908e9616030cc83d085989b8e6cd6df.tar.gz",
        "https://github.com/bazelbuild/rules_closure/archive/cf1e44edb908e9616030cc83d085989b8e6cd6df.tar.gz",  # 2019-04-04
    ],
)

# Tensorflow repo should always go after the other external dependencies.
# 2022-02-15
_TENSORFLOW_GIT_COMMIT = "a3419acc751dfc19caf4d34a1594e1f76810ec58"
_TENSORFLOW_SHA256 = "b95b2a83632d4055742ae1a2dcc96b45da6c12a339462dbc76c8bca505308e3a"
http_archive(
    name = "org_tensorflow",
    urls = [
      "https://github.com/tensorflow/tensorflow/archive/%s.tar.gz" % _TENSORFLOW_GIT_COMMIT,
    ],
    patches = [
        "@//third_party:org_tensorflow_compatibility_fixes.diff",
        # Diff is generated with a script, don't update it manually.
        "@//third_party:org_tensorflow_custom_ops.diff",
    ],
    patch_args = [
        "-p1",
    ],
    strip_prefix = "tensorflow-%s" % _TENSORFLOW_GIT_COMMIT,
    sha256 = _TENSORFLOW_SHA256,
)

load("@org_tensorflow//tensorflow:workspace3.bzl", "tf_workspace3")
tf_workspace3()
load("@org_tensorflow//tensorflow:workspace2.bzl", "tf_workspace2")
tf_workspace2()

# Edge TPU
http_archive(
  name = "libedgetpu",
  sha256 = "14d5527a943a25bc648c28a9961f954f70ba4d79c0a9ca5ae226e1831d72fe80",
  strip_prefix = "libedgetpu-3164995622300286ef2bb14d7fdc2792dae045b7",
  urls = [
    "https://github.com/google-coral/libedgetpu/archive/3164995622300286ef2bb14d7fdc2792dae045b7.tar.gz"
  ],
)
load("@libedgetpu//:workspace.bzl", "libedgetpu_dependencies")
libedgetpu_dependencies()

load("@coral_crosstool//:configure.bzl", "cc_crosstool")
cc_crosstool(name = "crosstool")
