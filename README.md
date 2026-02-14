# Chimera V5 - FIX Trading System

**Status:** ✅ Working Build - Ready to Compile

## Download

**[ChimeraV5.tar.gz](ChimeraV5.tar.gz)** (549 KB)

## What's Inside

- Full FIXSession API (restored from working backup)
- All governance removed from FIX layer  
- Correct FIXMessage usage (encode/parseZeroCopy)
- Missing includes added
- MSVC-safe CMake
- Metals only: XAUUSD + XAGUSD

## Build

```powershell
# Windows
tar -xzf ChimeraV5.tar.gz
cd ChimeraV5
mkdir build && cd build
cmake .. -G "Visual Studio 17 2022" -A x64
cmake --build . --config Release
```

```bash
# Linux
tar -xzf ChimeraV5.tar.gz
cd ChimeraV5
mkdir build && cd build
cmake ..
make -j4
```

## Requirements

- CMake 3.15+
- OpenSSL 3.x
- Visual Studio 2022 (Windows) OR GCC 9+ (Linux)

## Architecture

```
main.cpp
    ↓
ExecutionAuthority (governance - metals only)
    ↓
CTraderFIXClient (dual session orchestration)
    ↓
FIXSession (pure transport - NO governance)
    ↓
FIXSSLTransport
```

**Generated:** 2026-02-14
