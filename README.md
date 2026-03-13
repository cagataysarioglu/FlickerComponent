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
4. **Usage examples**
   ```cpp
   // In Blueprint or C++
   // Start flickering with blue-green light
   FlickerComponent->SetBaseIntensity(1453.0f);
   FlickerComponent->SetBaseColor(FLinearColor(0.2f, 0.8f, 1.0f));
   FlickerComponent->StartFlicker();

   // Stop after 3 seconds
   FTimerHandle TimerHandle;
   GetWorld()->GetTimerManager().SetTimer(TimerHandle, [this]() 
   {
       FlickerComponent->StopFlicker();
   }, 3.0f, false);

   // Play a predefined sequence (created in Blueprint)
   FlickerComponent->PlayNamedSequence(TEXT("ExplosionWarning"));

   // Create dynamic sequence (5 flickers, 0.2s each, 10% intensity)
   FlickerComponent->PlayFlickerSequence(5, 0.2f, 0.1f);

   // Stop current sequence
   FlickerComponent->StopSequence();

   // Play a named timeline
   FlickerComponent->PlayTimeline(TEXT("FadeToBlack"));

   // Timeline controls
   if (FlickerComponent->GetCurrentMode() == EFlickerMode::Timeline)
   {
       FlickerComponent->SetTimelinePaused(true); // Pause
       FlickerComponent->SetTimelinePaused(false); // Resume
    
       // Jump to specific time (actual time, not normalized)
       float Duration = FlickerComponent->GetTimelineDuration();
       FlickerComponent->SetTimelineTime(Duration * 0.5f); // Go to halfway
    
       FlickerComponent->StopTimeline(); // Stop completely
   }

   // Customize flicker behavior
   FFlickerSettings CustomSettings;
   CustomSettings.DipChanceMultiplier = 2.0f; // More frequent dips
   CustomSettings.DipStrength = 2.0f; // Deeper dips
   CustomSettings.MicroJitterStrength = 0.5f; // Medium micro-flicker
   CustomSettings.BlackoutChanceMultiplier = 1.5f; // More blackouts
   CustomSettings.ColorChangeSpeed = 2.0f; // Faster color changes
   CustomSettings.ColorVariationStrength = 0.3f; // Color variation

   FlickerComponent->SetSettings(CustomSettings);
   FlickerComponent->StartFlicker();

   // Disable specific light by tag
   FlickerComponent->SetLightEnabled(TEXT("EmergencyLight"), false);

   // Add custom settings for a single light
   FFlickerLightSettings DeskLampSettings;
   DeskLampSettings.LightTag = TEXT("DeskLamp");
   DeskLampSettings.bOverrideColor = true;
   DeskLampSettings.CustomColor = FLinearColor::Yellow;
   DeskLampSettings.MicroJitterStrength = 0.2f; // Less flicker

   FlickerComponent->AddLightSettings(TEXT("DeskLamp"), DeskLampSettings);

   // Remove settings
   FlickerComponent->RemoveLightSettings(TEXT("DeskLamp"));

   // Clear all per-light settings
   FlickerComponent->ClearLightSettings();

   // Audio settings (enabled by default)
   FlickerComponent->bEnableBuiltInAudio = true;
   FlickerComponent->bUseDistanceBasedAudio = true;
   FlickerComponent->AudioDistanceRadius = 1881.0f;

   // Force sync all clients (server only, for rare cases)
   if (GetOwner()->HasAuthority())
   {
       FlickerComponent->ForceSyncAllClients();
   }