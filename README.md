# NordicVoxel

Rust-basert voxel-motor med C#-API. Pipeline:

\[Rust core]\ → C ABI → \[C# wrapper/API]\ → dine .NET-spill/tools

## Kjappstart
1) Bygg Rust:
\\\ash
cd rust/voxel_core
cargo build --release
\\\

2) Kopiér native-lib til .NET-prosjektets \untimes/*/native\ (CI gjør dette for deg i Actions også).

3) Kjør demo:
\\\ash
cd ../../dotnet/VoxelEngine
dotnet run
\\\

MIT-lisens. Bidrag velkomne 💙
