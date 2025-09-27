# AppJB.Ciber — WPF + MVVM + EF Core + SQLite

Sistema de Gestión de Ciber (Videojuegos El Profe 3.0). Arquitectura por capas con MVVM.

## Estructura
```
AppJB.Ciber/
├─ docs/                      # Documentación (plantilla ADOO + arquitectura)
├─ src/
│  ├─ AppJB.Ciber.Presentation     # WPF (Views + ViewModels + DI)
│  ├─ AppJB.Ciber.Application      # Servicios de aplicación (casos de uso)
│  ├─ AppJB.Ciber.Domain           # Entidades y contratos
│  └─ AppJB.Ciber.Infrastructure   # EF Core + SQLite (repos/DbContext)
└─ tests/
   └─ AppJB.Ciber.Tests
```

## Requisitos
- .NET 8 SDK
- Visual Studio 2022 (o VS Code con C# Dev Kit)

## Primeros pasos
```bash
git init
git add .
git commit -m "feat: repo inicial AppJB.Ciber (WPF+MVVM+EFCore)"
# Crea un repo en GitHub y pega el remote (ejemplo):
git remote add origin https://github.com/tu-usuario/AppJB.Ciber.git
git branch -M main
git push -u origin main
```

## Ejecutar
- Abre `AppJB.Ciber.sln` en Visual Studio.
- Proyecto de inicio: `AppJB.Ciber.Presentation`.
- Presiona F5.

## Migraciones EF Core (opcional luego)
```bash
# Desde src/AppJB.Ciber.Infrastructure
dotnet ef migrations add InitialCreate
dotnet ef database update
```

## Licencia
MIT
