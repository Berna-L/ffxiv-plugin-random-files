# How do I export resources (like audio files) when building my plugin?

If you have non-code files on your plugin that should be shipped with it, you must declare them in the project's `.csproj` file.

For example, the `Congratulations` plugin ships with four sounds,
[all of them inside the project's `Sounds` folder](https://github.com/Berna-L/ffxiv-congratulations-plugin/tree/master/Congratulations/Sounds).

For them to be output with the plugin's DLL when it's built, [the following lines were added to the `.csproj`](https://github.com/Berna-L/ffxiv-congratulations-plugin/blob/master/Congratulations/Congratulations.csproj#L71-L84):

```xml
<ItemGroup>
    <None Update="Sounds\one-third.mp3">
        <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="Sounds\two-thirds.mp3">
        <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="Sounds\three-thirds.mp3">
        <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="Sounds\all-seven.mp3">
        <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
</ItemGroup>
```
