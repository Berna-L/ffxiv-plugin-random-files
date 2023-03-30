# Added NAudio to my project, but the build failed and there's something about WindowsForms in there...

This happens because the full `NAudio` NuGet package includes some dependencies on Windows Forms,
which breaks on non-Windows systems (like the one used on Plogon Build).

You have two options:

## Add `<EnableWindowsTargeting>true</EnableWindowsTargeting>` to your project's `.csproj`

What it says on the tin.
Add `<EnableWindowsTargeting>true</EnableWindowsTargeting>` to your project's `.csproj`
and Plogon Build will be able to build it.

## Use only the NAudio subpackages needed for your project

If you know exactly which NAudio subpackages have the classes and methods you need
to play the types of audio you want to play, remove the full `NAudio` package
from your dependencies and add the desired subpackages.

For example, `NAudio.Wasapi` is enough to play .WAV and .MP3 files
(just use the `PlaySound` implementation used [here](https://github.com/Berna-L/ffxiv-tf2-crit-plugin/blob/73ca0a42a052e74b7caf750feb3be2aa20affdaf/Tf2CriticalHitsPlugin/SoundEngine.cs)).
