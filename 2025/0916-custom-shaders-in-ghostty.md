# 0916-custom shaders in ghostty

* install ghostty

```
brew install --cask ghostty
```

* download shaders (.glsl file) from [https://github.com/KroneCorylus/ghostty-shader-playground/tree/main/shaders](https://github.com/KroneCorylus/ghostty-shader-playground/tree/main/shaders)
* add config in ghostty

```
custom-shader = /Users/pointsource/.config/ghostty/shader_smear.glsl
custom-shader-animation = "true"
```

* reload config
