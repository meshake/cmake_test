# Build missing dependencies in Release mode

conan install --install-folder release --settings build_type=Release --profile proto32-win --build=missing .

# Build missing dependencies in Debug mode

conan install --install-folder debug --settings build_type=Debug --profile proto32-win --build=missing .

# Generate Ninja build files (run inside release or debug directory)
cmake build -GNinja ..

ninja test-proto

# Generate Makefiles (run inside release or debug directory)
cmake build -G"Unix Makefiles" ..

make test-proto
