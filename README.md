# Batman Villains Drag & Drop - Blazor WebAssembly Application

A interactive drag-and-drop application built with **Blazor WebAssembly** featuring Batman villains with two distinct drag-and-drop experiences implemented entirely in C# without JavaScript.

## 🦇 Overview

This application demonstrates modern web development using Blazor WebAssembly, showcasing multiple drag-and-drop patterns without requiring JavaScript. Users can intuitively manage Batman villains through two different interfaces:

1. **Container Management**: Move villains between "Available Villains" and "Active Threat List" containers
2. **List Reordering**: Drag and drop to reorder villains within a prioritized list

## ✨ Features

### 🏠 Home Page - Container Drag & Drop
- **Two-Container Interface**: Drag villains between "Available Villains" and "Active Threat List"
- **Visual Feedback**: Cards highlight during drag operations
- **Empty State Handling**: Clear messaging when threat list is empty
- **Bidirectional Movement**: Move villains back and forth between containers

### 📋 Villain List Page - Reorder Drag & Drop
- **List Reordering**: Drag and drop to reorder villains by priority/preference
- **Visual Drag Indicators**: Dragged items show rotation and opacity effects
- **Drop Target Highlighting**: Clear visual feedback for valid drop zones
- **Drag Handles**: Visual indicators (⋮⋮) to show draggable areas
- **Smooth Animations**: CSS transitions for enhanced user experience

### 🎨 Common Features
- **Responsive Design**: Built with Bootstrap for mobile and desktop compatibility
- **No JavaScript Required**: Pure C# implementation using Blazor's event handling
- **Rich Villain Data**: Detailed descriptions for each Batman villain
- **Progressive Web App (PWA)**: Includes service worker for offline capabilities

## 🚀 Technology Stack

- **.NET 9.0**: Latest .NET framework
- **Blazor WebAssembly**: Client-side web UI framework
- **C# 13.0**: Modern C# language features
- **Bootstrap 5**: Responsive CSS framework
- **HTML5 Drag and Drop API**: Native browser drag-and-drop support
- **Progressive Web App (PWA)**: Service worker enabled

## 🏗️ Blazor Implementation Details

### Component Architecture

The application leverages Blazor's component-based architecture:

- **`Home.razor`**: Container-based drag-and-drop (villains ↔ threats)
- **`VillainList.razor`**: Single-list reordering drag-and-drop
- **`Villain.cs`**: Simple model class representing villain data
- **Scoped CSS**: Component-specific styling with `.razor.css` files

### Key Blazor Features Demonstrated

1. **Event Handling**: 
   - `@ondragstart`, `@ondragend`, `@ondrop`, `@ondragover`, `@ondragleave`
   - Event callbacks with lambda expressions
   - `@ondragover:preventDefault="true"` for proper drop zones

2. **Data Binding**:
   - Two-way binding with `List<Villain>` collections
   - Dynamic UI updates with `StateHasChanged()`
   - Real-time list manipulation and reordering

3. **Conditional Rendering**:
   - `@if` statements for empty state messages
   - Dynamic CSS class binding with `@(condition ? "class" : "")`
   - `@foreach` loops for dynamic content generation

4. **Component Lifecycle**:
   - `OnInitialized()` override for data initialization

### Drag & Drop Implementations

#### Home Page - Container Switching
The container-based drag-and-drop uses a simple state tracking approach:

```csharp
private void HandleDragStart(Villain villain)
{
    DraggedVillain = villain;
    DraggedFromContainer = AvailableVillains.Contains(villain) ? "available" : "threats";
}

private void HandleDrop(string targetContainer)
{
    // Remove from source, add to target
    if (targetContainer == "threats")
        ThreatVillains.Add(DraggedVillain);
    // ... cleanup and state update
}
```

#### Villain List Page - Reordering
The reordering implementation uses index-based tracking:

```csharp
private void OnDrop(int index)
{
    if (draggedIndex != -1 && draggedIndex != index)
    {
        var draggedVillain = villains[draggedIndex];
        villains.RemoveAt(draggedIndex);
        
        var targetIndex = draggedIndex < index ? index - 1 : index;
        villains.Insert(targetIndex, draggedVillain);
    }
}
```

## 🎭 Batman Villains Featured

The application includes detailed information about iconic Batman villains:

- **The Joker** - The Clown Prince of Crime
- **Harley Quinn** - Former psychiatrist turned chaotic accomplice  
- **The Penguin** - Sophisticated crime lord with bird obsession
- **The Riddler** - Puzzle-obsessed criminal mastermind
- **Two-Face** - Former DA with dual personality disorder
- **Poison Ivy** - Plant-loving eco-terrorist
- **Scarecrow** - Fear-obsessed psychiatrist
- **Mr. Freeze** - Cryogenic criminal
- **Bane** - The man who broke Batman's back
- **Catwoman** - Master thief walking the line between hero and villain
- **Ra's al Ghul** - Immortal leader of the League of Assassins *(Home page only)*
- **Clayface** - Shape-shifting clay monster *(Home page only)*

## 🚀 Getting Started

1. **Prerequisites**: .NET 9.0 SDK
2. **Clone the repository**
3. **Run the application**:
   ```bash
   dotnet run
   ```
4. **Navigate to**:
   - **Home** (`/`) - Container drag & drop experience
   - **Batman Villains** (`/villainList`) - List reordering experience

## 📱 Navigation

- **Home**: Container-based villain management
- **Batman Villains**: Single list reordering interface  
- **Weather**: Standard Blazor template page (not villain-related)

## 🎯 Learning Objectives

This project demonstrates:

- **Multiple Drag & Drop Patterns**: Container switching vs. list reordering
- **Pure Blazor Implementation**: No JavaScript dependencies
- **HTML5 Drag and Drop API**: Proper event handling in Blazor
- **State Management**: Tracking drag operations and UI updates
- **Component Architecture**: Separation of concerns with multiple pages
- **CSS Integration**: Visual feedback and responsive design
- **Modern .NET Features**: C# 13.0 and .NET 9.0 capabilities

Perfect for developers learning Blazor WebAssembly, drag-and-drop interfaces, and modern .NET web development patterns.
