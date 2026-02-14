# Chimera V5 - VERSION-CONSISTENT FIX Build

**Status:** ✅ Single-Version Architecture - No Mixed APIs

## CRITICAL CHANGE

**Download this instead:** **[ChimeraV5_CONSISTENT.tar.gz](ChimeraV5_CONSISTENT.tar.gz)** (542 KB)

### What Was Wrong Before

The previous package had files from DIFFERENT VERSIONS mixed together:
- FIXConfig expected `tradePort` and `pricePort`
- But some code used `port`
- FIXMessage had `encode()` but some code called `serialize()`
- CTraderFIXClient constructor took NO arguments
- But main.cpp tried to pass FIXConfig to constructor

**This caused 50+ compile errors from API mismatches.**

### What's Fixed Now

✅ **ALL files from same version**  
✅ **FIXConfig:** has `tradePort`, `pricePort`, `senderCompID`, etc  
✅ **FIXSession:** has `setConfig()`, `start(host, port)`, callbacks  
✅ **FIXMessage:** uses `encode()` and `parseZeroCopy()`  
✅ **CTraderFIXClient:** default constructor + `setConfig()` + `setOnExec()`  
✅ **main.cpp:** matches actual API  

## Build

```powershell
# Extract
tar -xzf ChimeraV5_CONSISTENT.tar.gz
cd (extracted directory)

# Build
mkdir build && cd build
cmake .. -G "Visual Studio 2022" -A x64
cmake --build . --config Release
```

## Requirements

- CMake 3.15+
- OpenSSL 3.x
- Visual Studio 2022 (Windows) OR GCC 9+ (Linux)

## Architecture

```
main.cpp
    ↓
ExecutionAuthority (metals-only governance)
    ↓
CTraderFIXClient
    ├─ TRADE Session (port 5212)
    └─ QUOTE Session (port 5211)
    ↓
FIXSession (clean transport)
    ↓
FIXSSLTransport
```

**All components from ONE consistent codebase.**

---

**Updated:** 2026-02-14 08:12 UTC  
**Status:** Version-consistent, ready to compile
