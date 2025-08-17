# Contributing

- Rust: \cargo fmt --all\, \cargo clippy -D warnings\
- .NET: \dotnet format\, \dotnet build -c Release\
- Kjør demoen: \dotnet run\

Arkitektur: Rust \cdylib\ med C ABI → C# P/Invoke wrapper + safe API.
