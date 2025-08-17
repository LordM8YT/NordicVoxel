# NordicVoxel

**NordicVoxel** is an open-source experimental voxel engine written in **Rust** with a safe and friendly **C# API**.  
The goal is to combine Rust’s safety and performance with the accessibility of .NET, allowing game developers and toolmakers to build voxel-based projects quickly.

```
[Rust core] → C ABI → [C# wrapper/API] → your .NET apps/games
```

---

## ✨ Features

- **Cross-language design** – Core engine in Rust, exposed via a C ABI, wrapped in C# for easy use.  
- **Chunk-based voxel world** – Fixed-size chunks for infinite terrain streaming.  
- **Naive face meshing** – Each visible voxel face produces a quad (to be extended later).  
- **Cross-platform** – Builds on Windows, Linux, and macOS.  
- **CI ready** – GitHub Actions automatically build and test on all three platforms.  

Planned:
- Greedy meshing (reduced poly count by 10–30×)  
- LOD support  
- Streaming and caching of chunks  
- Multithreaded meshing  
- Material atlas system  
- Optional Rust-side rendering via `wgpu`  

---

## 📂 Project Structure

```
NordicVoxel/
├─ rust/voxel_core/           # Rust cdylib: voxel engine core + C-ABI
│  ├─ Cargo.toml
│  └─ src/lib.rs
├─ dotnet/VoxelEngine/        # C# API wrapper using P/Invoke
│  ├─ VoxelEngine.csproj
│  ├─ Native.cs
│  ├─ Engine.cs
│  └─ Program.cs (demo)
├─ .github/workflows/ci.yml   # GitHub Actions CI
├─ README.md
├─ LICENSE
└─ CONTRIBUTING.md
```

---

## 🚀 Getting Started

### Prerequisites
- Rust (stable, v1.75+ recommended)  
- .NET 8 SDK  

### 1. Build the Rust core
```bash
cd rust/voxel_core
cargo build --release
```

This produces a native library:
- `voxel_core.dll` (Windows)  
- `libvoxel_core.so` (Linux)  
- `libvoxel_core.dylib` (macOS)  

### 2. Copy the native library into the .NET project
Copy the compiled library into:

```
dotnet/VoxelEngine/runtimes/win-x64/native/voxel_core.dll
dotnet/VoxelEngine/runtimes/linux-x64/native/libvoxel_core.so
dotnet/VoxelEngine/runtimes/osx-arm64/native/libvoxel_core.dylib
```

(Use the correct runtime folder for your system.)

### 3. Run the C# demo
```bash
cd ../../dotnet/VoxelEngine
dotnet run
```

Expected output (example):
```
ChunkSize: 16
Verts: 1234 (floats: 9872)
Indices: 2468
v0: pos=(0, 0, 0) n=(0, 1, 0) uv=(0, 0)
```

---

## 🛠️ Development Workflow

**Rust**
```bash
cargo fmt --all
cargo clippy --all-targets --all-features -D warnings
cargo build --release
```

**.NET**
```bash
dotnet format
dotnet build -c Release
dotnet run
```

---

## 🧪 Example Usage

C# API:
```csharp
using VoxelEngine;

class Demo {
    static void Main() {
        using var eng = new Engine(16);
        var mesh = eng.GenerateChunkMesh((0, 0, 0));

        Console.WriteLine($"ChunkSize: {eng.ChunkSize}");
        Console.WriteLine($"Vertices: {mesh.VertexCount}");
        Console.WriteLine($"Indices: {mesh.IndexCount}");
    }
}
```

---

## 📦 Roadmap

- [x] Rust voxel core with C ABI  
- [x] C# wrapper API  
- [x] Naive chunk meshing  
- [ ] Greedy meshing  
- [ ] Chunk streaming  
- [ ] Multithreading  
- [ ] LOD support  
- [ ] Material atlas & textures  
- [ ] Optional rendering via Rust `wgpu`  

---

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.  
Open issues for bugs, features, or design discussions. PRs are encouraged.

---

## 📄 License

MIT License – see [LICENSE](LICENSE).  
You are free to use, modify, and distribute this software with attribution.

---

## 🙌 Acknowledgements

- Rustaceans 🦀 for safe performance  
- The .NET ecosystem for developer ergonomics  
- Open-source voxel engine research & community inspiration  
