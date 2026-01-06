# NixOS-Splash-Plasma6
![preview image of splash screen](./contents/previews/splash.png "preview")

NixOS splash screen for KDE Plasma 6

# Usage
Add NixOS-Splash-Plasma6 as a flake input to your system flake, usually `/etc/nixos/flake.nix`
```nix
nixos-splash-plasma6 = {
   url = "github:nimrodium/nixos-splash-plasma6";
   inputs.nixpkgs.follows = "nixpkgs";
};
```
Add it as an argument to outputs or attach `@inputs`, or in SOME way get it accessible to the output function and then pass it to your `nixosSystem`
```nix
specialArgs = { inherit nixos-splash-plasma6; }
```
or by just passing the entire inputs set (which is easier to use long-term).
```nix
specialArgs = { inherit inputs; }
```

In your system's `configuration.nix`, add the package to `environment.systemPackages`
```nix
environment.systemPackages = with pkgs; [
  inputs.nixos-splash-plasma6.packages.${pkgs.system}.default
]
```
then select it in Plasma's settings.

If you use [home-manager](https://github.com/nix-community/home-manager) with [plasma-manager](https://github.com/nix-community/plasma-manager/), you can select the splash screen declaratively like so:
```nix
programs.plasma.workspace.splashScreen = {
   engine = "KSplashQML";
   theme = "NixOS-Splash-Plasma6";
};
```

# Customization

## Changing the Splash Text

You can customize the splash screen text by overriding the `splashText` attribute:

```nix
environment.systemPackages = with pkgs; [
  (inputs.nixos-splash-plasma6.packages.${pkgs.system}.default.override {
    splashText = "Your Custom Text Here";
  })
]
```


---
forked from https://github.com/smokey5787/EOS-Splash-Plasma6
