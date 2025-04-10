# P2P-Chat Project

## Prerequisites

1. **Git**: [Install Git](https://git-scm.com/downloads)
2. **CMake**: [Install CMake](https://cmake.org/download/)
3. **Visual Studio** (or any IDE with CMake support) or **Visual Studio Code** with the CMake extension (optional, depending on your preference).
4. **vcpkg**: [Install vcpkg](https://github.com/microsoft/vcpkg)

## Setup Instructions

### 1. Clone the Repository
Clone the repository to your local machine:
```bash
git clone https://github.com/David-Krivoklatsky/P2P-Chat.git
cd P2P-Chat
```

### 2. Install vcpkg

> [!IMPORTANT]
> Ensure that **vcpkg** is properly installed before proceeding with the project setup. Missing dependencies may cause build failures.

If you don't have vcpkg installed, follow these steps:
Clone the vcpkg repository:

#### 1. Clone the vcpkg repository:
```bash
git clone https://github.com/microsoft/vcpkg.git
```

#### 2. Navigate to the vcpkg directory and build it:
```bash
cd vcpkg
.\bootstrap-vcpkg.bat  # On Windows
./bootstrap-vcpkg.sh  # On Linux/MacOS
```

#### 3. Add vcpkg to your PATH (optional but recommended for convenience):
- On **Windows**: Add C:\path\to\vcpkg to your PATH environment variable.
- On **Linux/MacOS**: Add export PATH=$PATH:/path/to/vcpkg to your .bashrc or .zshrc.

### 3. Install Project Dependencies

Now that vcpkg is set up, install the required dependencies for the project:

#### 1. Navigate to the project directory:

```bash
cd /path/to/your/P2P-Chat
```

#### 2. Install the dependencies using vcpkg:

```bash
cd ..
vcpkg install boost-beast:x64-windows
vcpkg install nlohmann-json:x64-windows
vcpkg install termcolor:x64-windows
```

### 4. Set Up the CMake Configuration

#### 1. Create a new build directory:

```bash
mkdir build
cd build
```

#### 2. Configure the CMake project with the vcpkg toolchain file:

- To run in **Command prompt**:
    ```cmd
    cmake .. -DCMAKE_TOOLCHAIN_FILE=%VCPKG_ROOT%/scripts/buildsystems/vcpkg.cmake
    ```
- To run in **Powershell**:
    ```powershell
    cmake .. -DCMAKE_TOOLCHAIN_FILE="$env:VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake"
    ```

Make sure the path to `vcpkg.cmake` is correct.

### 5. Build the Project

Once CMake configuration completes, build the project by running:

```bash
cmake --build . --config Debug   # Or 'Release' depending on your configuration
```

> [!TIP]
> If you encounter build errors related to missing libraries, make sure that all the required dependencies are installed using **vcpkg**.

### 6. Run the Project

After building, you can run the project directly from the command line or through your IDE:

To run from the command line:

```bash
./bin/your_executable_name    # Adjust the path if needed
```

<!-- In **Visual Studio**, press `F5` to start debugging, or choose **Debug → Start Debugging**. -->

> [!INFO]
> If you are using **Visual Studio**, you can simply press **`F5`** to build and run the project after configuring it with CMake, or choose **Debug → Start Debugging**.

## Rebuilding the Project

If you need to rebuild the project later, you can simply run the following commands from the build directory:

```bash
cmake --build . --config Debug  # Or 'Release' based on your build configuration
```

To clear the CMake cache and regenerate the project:

```bash
rm -rf CMakeCache.txt CMakeFiles/
cmake ..
```

## Additional Notes

- **vcpkg and CMake Compatibility:** Ensure that the **vcpkg toolchain** is properly set in the CMake configuration. This is done by passing `-DCMAKE_TOOLCHAIN_FILE` when running `cmake`.

- **Windows and Linux Setup:** The setup steps are similar for both systems, except for the path to the **vcpkg toolchain** file and the command to run **vcpkg** itself.