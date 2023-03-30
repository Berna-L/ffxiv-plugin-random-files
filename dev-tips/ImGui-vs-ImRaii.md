# Prefer using ImRaii instead of ImGui to push styles and colors

ImRaii, by Otter and available as part of Dalamud.Interface (declaration below),
makes it harder to forget to pop styles and colors from ImGui, which can have (literally) ugly consequences.

How to use:

## When the push happens inside a method and the pop at the end of the method:

```csharp
  public void Draw() {
    //draw not stylish things here
    // don't forget the "using" keyword!
    using var stylePush = ImRaii.PushStyle(ImGuiStyleVar.WindowBorderSize, 0f);
    //draw stylish things here
  }
```

When the method finishes, `using` will make it so `stylePush.Dispose()` is called, which will take care of popping.

## When the push happens inside a method, but the pop should happen before it ends:

```csharp
  public void Draw() {
    //draw not stylish things here
    using (ImRaii.PushStyle(ImGuiStyleVar.WindowBorderSize, 0f)) {
      // draw stylish things here 
    }
    //draw more not stylish things here
  }
```

The `Dispose()` method on the object being "used" will be called after the `using` block ends, popping the style/color.

## When the push happens in one method and the pop happens in another
This usually happens when you are setting styles/colors in a window on `PreDraw()`, and removing those styles/colors on `PostDraw()`.

```csharp
public class ColorfulWindow: Window {
  
  private ImRaii.Color? windowBg;
  
  //ctor and other stuff
  
  public override void PreDraw() {
    windowBg = ImRaii.PushColor(ImGuiCol.WindowBg, new Vector2(1f, 1f, 1f, 1f));
  }
  
  public override void PostDraw() {
    windowBg?.Dispose();
  }
}
```

`Dalamud.Interface` declaration (to add to your plugin project's `.csproj`):

```xml
    <ItemGroup>
        <Reference Include="Dalamud.Interface">
            <HintPath>$(DalamudLibPath)Dalamud.Interface.dll</HintPath>
            <Private>false</Private>
        </Reference>
    </ItemGroup>
```
