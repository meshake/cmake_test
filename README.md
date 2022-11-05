# Conan: Build and install dependencies
## Build missing dependencies in Release mode
conan install --install-folder release --settings build_type=Release --profile profiles/proto32-linux --build=missing .

## Build missing dependencies in Debug mode
conan install --install-folder debug --settings build_type=Debug --profile profiles/proto32-linux --build=missing .

# cmake: generate build files
## Linux
cmake -S . -B release -GNinja

or

cmake -S . -B release -G"Unix Makefiles"

## Windows
cmake -S . -B release -G"Visual Studio 17 2022"

# cmake: build
## Linux
cmake --build release --config Release

or

cd release && ninja MyProject

or

cd release && make MyProject

## Windows
cmake --build release --target MyProject --config Release
