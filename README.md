# SpySatellite
Managed code inject through satellite assembly.

## Intro
[Satellite assemblies](https://docs.microsoft.com/en-us/dotnet/core/dependency-loading/loading-resources) are used to store localized resources customized for language and culture.

A satellite assembly will be loaded by `ResouceManager` when the program is going to fetch culture specific resources, e.g. localization texts.

Usually a satellite assembly only contains resources, not code. Even if you added code in it - no matter using a module initializer or a static constructor, the code won't be executed when the assembly is loaded by `ResourceManager`.

However, with this technique (`SpySatellite`), it's still possible to run code when a satellite assembly is loaded.

## Why
There are many powerful code injection techniques in .NET world, such as `Harmony`.

SpySatellite is just a PoC to prove it's possible to make use of satellite assemblies. There are some interesting points:

1. People usually don't expect there is code hidden in a satellite assembly.
2. The strong name of satellite assemblies is not strictly checked. A modified satellite assembly can still be loaded.
3. Satellite assemblies can be provided by a 3rd party - such as translators or plugin makers. With this technique, they can add license check or malicious code into the main program.

---

by Ulysses (wdwxy12345@gmail.com)