# Soc Ops Workspace Guidelines

## Overview
Soc Ops is a Blazor WebAssembly social bingo game. This document provides coding standards and conventions for all agents working in this workspace.

## Code Style

### C# / Razor Conventions
- Use **implicit namespaces** and **nullable reference types** (enabled in `.csproj`)
- Component logic: Use **event handlers** with `@on*` directives (e.g., `@onclick`)
- Service injection: Use `[Inject]` attribute or constructor injection in Razor components
- Return types: Prefer `Task` and `Task<T>` for async operations
- Naming: Pascal case for public members, camelCase for private fields

### Razor Component Structure
```
@page "/route"
@namespace SocOps.Components

<Layout HTML>

@code {
    // Properties/Fields
    // Lifecycle methods (OnInitialized, OnParametersSet)
    // Event handlers
    // Helper methods
}
```

## Architecture

### Folder Organization
- **`Components/`**: UI components (BingoBoard, BingoSquare, GameScreen, etc.)
- **`Services/`**: Business logic (BingoGameService, BingoLogicService)
- **`Data/`**: Static data and models (Questions.cs)
- **`Models/`**: Data classes (BingoSquareData, GameState, BingoLine)
- **`Layout/`**: Navigation and page layout (MainLayout, NavMenu)
- **`Pages/`**: Routable pages (Home, Counter, Weather, NotFound)

### Service Pattern
- Services are registered in `Program.cs` with `.AddScoped<T>()`
- Injected into components via `[Inject] ServiceType Service { get; set; }`
- Encapsulate game logic; keep components focused on presentation

## Build and Test

### Build Commands
```bash
cd SocOps
dotnet build                    # Build with debug configuration
dotnet run                      # Build and run dev server (http://localhost:5166)
```

### Development Workflow
1. Components auto-reload on file save
2. Services require full app restart to reflect changes
3. Use browser DevTools (F12) for debugging rendered output
4. Check `.NET Debug` tab in VS Code for breakpoints

## Conventions

### Styling
- Use **CSS utility classes** from `wwwroot/css/app.css` (similar to Tailwind)
- Key utilities: `flex`, `grid`, `p-*`, `mb-*`, `bg-*`, `text-*`, `rounded-*`, `shadow-*`
- Custom colors: `.bg-accent` (primary blue), `.bg-marked` (selected green)
- See `.github/instructions/css-utilities.instructions.md` for full reference

### Frontend Design
- When designing components: Create distinctive, polished UIs—avoid generic AI aesthetics
- Use typography and color deliberately; commit to a cohesive visual theme
- Leverage CSS-only animations for micro-interactions (no JavaScript)
- Reference `.github/instructions/frontend-design.instructions.md` for design patterns

### Game Logic
- **BingoGameService**: Manages game state, turn tracking, win detection
- **BingoLogicService**: Calculates bingo lines, validates winning patterns
- **Models**: GameState (active game), BingoSquareData (question + marked status), BingoLine (5-in-a-row)

### Component Patterns
- Use `@if` directives for conditional rendering (no hidden elements)
- Bind component state with `@bind` for two-way binding or `@onchange` for handlers
- Pass data to child components via `[Parameter]` attributes
- Emit events from child to parent using `EventCallback`

## Quick Links
- **Lab Guide**: See `workshop/` folder or hosted docs
- **CSS Utilities**: `.github/instructions/css-utilities.instructions.md`
- **Frontend Design**: `.github/instructions/frontend-design.instructions.md`
- **Project README**: README.md for setup and deployment info
- **Dev Server**: Runs on http://localhost:5166 after `dotnet run`

## Important Notes
- Target framework: **.NET 10.0**
- Framework: **Blazor WebAssembly** (not Server)
- No external dependency management frameworks (custom CSS utilities, no npm)
- Game deploys automatically to GitHub Pages on push to `main`
