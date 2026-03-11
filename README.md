# Flicker Component
Advanced flicker component for Unreal Engine with multiplayer support, RGB color cycling, custom sequences, and keyframe-based timeline system. Features per-light settings, sound system, and performance optimization.

## FEATURES
- **Multiplayer Ready** - Server-authoritative, syncs across all clients  
- **RGB Color Cycling** - Smooth color transitions during flicker  
- **Custom Sequences** - Create any flicker pattern (7 times, alarm sequences, etc.)  
- **Timeline System** - Advanced keyframe-based animation with curve support  
- **Per-Light Settings** - Control each light individually with tags  
- **Sound System** - Built-in audio with distance-based playback  
- **Performance Optimized** - Adjustable tick rate (10-120 fps)  
- **Full Blueprint Support** - Easy to use, no coding required  
- **State Restoration** - Automatically returns to previous state  
- **Multiple Easing Functions** - Linear, Sinusoidal, Ease In/Out, etc.  

## REQUIREMENTS
- Unreal Engine 5.0+
- Visual Studio 2022 (for C++ projects)
- Basic knowledge of Unreal Engine lighting system

## QUICK START
1. **Install the plugin**
   - Copy `FlickerComponent` folder to your project's `Plugins` directory
   - Or install via Unreal Engine Marketplace
2. **Enable the plugin**
   - Open your project
   - Go to `Edit → Plugins`
   - Search for the component and enable it
   - Restart the editor
3. **Add to your actor**
   - Select any actor with a light component
   - Click `Add Component` → Search for the component
   - Or drag-drop from the plugin menu
4. **Basic usage**
   ```cpp
   // In Blueprint or C++
   FlickerComponent->SetBaseIntensity(400.0f);
   FlickerComponent->StartFlicker();