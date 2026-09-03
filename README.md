```txt
aoi-cpp/
├── godot-cpp/              # Git Submodule (Clone từ repo chính thức của Godot)
├── include/                # Public Headers (.hpp)
│   ├── Core/
│   ├── Performance/
│   ├── Algorithms/
│   └── Platform/
├── src/                    # Source Files (.cpp)
│   ├── Core/
│   ├── Performance/
│   ├── Algorithms/
│   ├── Platform/
│   │   └── Android/        # JNI / Android NDK specific code
│   └── GDExtension/        # Binding code, register_types.cpp
├── bin/                    # Output Directory (Sẽ copy sang Godot Project)
│   ├── android/            # libaoi_core.android.arm64.so
│   └── windows/            # libaoi_core.windows.x86_64.dll
├── SConstruct              # Build script cho SCons (Tiêu chuẩn của godot-cpp)
├── CMakeLists.txt          # (Optional) Nếu bạn dùng CMake thay vì SCons
└── aoi_core.gdextension    # File cấu hình để Godot nhận diện thư viện
```
