# Soc Ops Workspace Guidelines

## ✅ Mandatory Development Checklist
Before committing, ensure:
- [ ] **Lint**: Code follows C#/Razor conventions (implicit namespaces, nullable types)
- [ ] **Build**: `dotnet build` passes without warnings
- [ ] **Test**: Changes tested locally via `dotnet run` (http://localhost:5166)

---

## Code Style

**C# / Razor:**
- Implicit namespaces & nullable reference types (enabled in `.csproj`)
- Event handlers: `@on*` directives (e.g., `@onclick`)
- Service injection: `[Inject]` attribute
- Pascal case for public, camelCase for private

**Component Structure:**
```razor
@page "/route"
@namespace SocOps.Components

<HTML>

@code { /* Logic */ }
```

## Architecture

**Folder Organization:**
- `Components/`: UI (BingoBoard, BingoSquare, GameScreen)
- `Services/`: Logic (BingoGameService, BingoLogicService)
- `Models/`: Data classes (GameState, BingoSquareData, BingoLine)
- `Data/`: Static data (Questions.cs)
- `Layout/`, `Pages/`: Routes & navigation

**Service Pattern:** Registered in `Program.cs` with `.AddScoped<T>()`, injected via `[Inject]`. Keep logic in services, presentation in components.

## Build & Development

```bash
cd SocOps
dotnet build                # Debug build
dotnet run                  # Dev server (http://localhost:5166)
```

**Workflow:** Components auto-reload on save. Services require app restart. Use F12 DevTools or `.NET Debug` tab for debugging.

## Conventions

**Styling:** CSS utility classes in `wwwroot/css/app.css` (Tailwind-like). Key utilities: `flex`, `grid`, `p-*`, `mb-*`, `bg-*`, `text-*`, `rounded-*`, `shadow-*`. Custom: `.bg-accent` (blue), `.bg-marked` (green).

**Frontend Design:** Create distinctive, polished UIs. Avoid generic AI aesthetics. Use intentional typography/color. CSS-only animations. See `.github/instructions/frontend-design.instructions.md`.

**Game Logic:** `BingoGameService` manages state & win detection. `BingoLogicService` calculates bingo lines. Models: `GameState`, `BingoSquareData`, `BingoLine`.

**Components:** Use `@if` for conditional render. Bind with `@bind` or `@onchange`. Pass data via `[Parameter]`. Emit events with `EventCallback`.

## Quick Reference

- **Lab Guide**: `workshop/` folder or [hosted docs](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/)
- **CSS Utilities**: `.github/instructions/css-utilities.instructions.md`
- **Frontend Design**: `.github/instructions/frontend-design.instructions.md`
- **README**: Project setup & deployment info

**Stack:** .NET 10.0 • Blazor WebAssembly • Custom CSS utilities (no npm) • Auto-deploy to GitHub Pages on `main` push
