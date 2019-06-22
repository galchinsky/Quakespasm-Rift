# Virtual prism mod for Quakespasm-Rift

This is a fork of "Quuke for Oculus Rift" with a couple of patches for people with strabismus and amblyopia. This gives a chance to play Oculus without prismatic correction glasses and achieve stronger fusion due to contrast penalization of working eye (as https://onlinelibrary.wiley.com/doi/full/10.1111/opo.12123 suggested). I'd like to share this but note that you use it on your own risk.

I added 4 simple console commands and use it this way:

* Run the game. Quakespasm-Rift runs in VR-mode by default. If it starts in normal mode, enable 3rd party software in Oculus setup, also I have to run the app as administrator
* The game should load straight into the very first map where there are no monsters and this is useful for initial setup.
* Call the quake console using "~" button.
* First, you should set different contrast for your lazy and fellow eyes. Lazy eye should be penalized with lower contrast. My right eye is lazy so I type:

```
vr_contrast_left 0.1
vr_contrast_right 1.0
```

If your left eye is lazy you can type

```
vr_contrast_left 1.0
vr_contrast_right 0.1
```

You should start to experience double vision even if you have some sort of amblyopia and the lazy eye is suppressed, thanks to contrast penalization. If you have alternating strabismus, I would recommend to penalize one eye to achieve stronger double vision.

* When you see double vision, you are ready to set up your virtual prisms. There are 2 commands, `vr_angle_y` for horizontal correction (more common) and `vr_angle_x` for vertical correction. You should type them and check the 3d surrounding. The first level has convenient portal, lights and other objects. After some experiments, I use the following commands:

```
vr_angle_y 22
vr_angle_x -4
```

You can set non-integer angle: `vr_angle_y 9.5`

So, I added only 4 commands: `vr_contrast_left`, `vr_contrast_right`, `vr_angle_x`, `vr_angle_y`.

## Building without IDE

If you want to patch something without installing a monstrous 10 GB Microsoft IDE, there is a way to overcome this

1. Install "Visual C++ 2015 Build Tools". Set up `VS140COMNTOOLS` environment variable to `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools`
2. Go to https://developer.oculus.com/downloads/pc/1.9.0/Oculus_SDK_for_Windows/ then download and extract it NEXT TO (not in) your Quakespasm-Rift folder. So there is an "OculusSDK" folder and a "QuakeSpasm-Rift" folder side-by-side.
2. Run `cmd.exe`, cd to `c:\Program Files (x86)\MSBuild\14.0\Bin` and run `MSBuild [path-to]\Quakespasm-Rift\Windows\VisualStudio\quakespasm.sln /property:Configuration=Release`. It will build to `[path-to]\Quakespasm-Rift\Windows\VisualStudio\Build-quakespasm-sdl2\x86\Release`. I'm able to build only sdl version, the other one produces a lot of errors.
3. Copy `id1` with Quakesparm-Rift config and game file from https://github.com/phoboslab/Quakespasm-Rift/releases 

# Quake for Oculus Rift

[Download Here](https://github.com/phoboslab/Quakespasm-Rift/releases)

Based on [Quakespasm](http://quakespasm.sourceforge.net/). This enables support for the Oculus Rift CV1 in Direct Mode for idsoftware's original Quake. You need the Oculus SDK 1.9.0 and SDL to compile this.

More info: http://phoboslab.org/log/2016/05/quake-for-oculus-rift

The release version comes with a sensible `config.cfg` and `autoexec.cfg` file that enables VR Mode by default, disables view bobbing and sets the texture mode to NEAREST for the proper, pixelated oldschool vibe.

## Building:

1. Install the free Visual Studio 2015 Community Edition, if you don't already have it.

2. Go to https://developer.oculus.com/downloads/pc/1.9.0/Oculus_SDK_for_Windows/ then download and extract it NEXT TO (not in) your Quakespasm-Rift folder. So there is an "OculusSDK" folder and a "QuakeSpasm-Rift" folder side-by-side.

3. Use the VC13 solution to compile what you need:
	Quakespasm-Rift\Windows\VisualStudio\quakespasm.sln
	
4. In Visual Studio, right click project quakespasm-sdl2, click Properties. Set Configuration to All Configurations. Choose Debugging, set Working Directory to your Quake folder.

5. Run the quakespasm-sdl2 project. You need to enable VR in the game options and start a new game before it will be in VR.

## Additional cvars:
- `vr_enabled` – 0: disabled, 1: enabled
- `vr_crosshair` – 0: disabled, 1: point, 2: laser sight
- `vr_crosshair_size` - Sets the diameter of the crosshair dot/laser from 1-32 pixels wide. Default 3.
- `vr_crosshair_depth` – Projection depth for the crosshair. Use `0` to automatically project on nearest wall/entity. Default 0.
- `vr_crosshair_alpha` – Sets the opacity for the crosshair dot/laser. Default 0.25.
- `vr_aimmode` – 1: Head Aiming, 2: Head Aiming + mouse pitch, 3: Mouse aiming, 4: Mouse aiming + mouse pitch, 5: Mouse aims, with YAW decoupled for limited area, 6: Mouse aims, with YAW decoupled for limited area and pitch decoupled completely. Default 1.
- `vr_deadzone` – Deadzone in degrees for `vr_aimmode 5`. Default 30.
- `vr_perfhud`- – Show the Oculus Performance Hud (1-5). Default 0.
- `snd_device` – Search string for the audio output device to use. Default: "default". This will get set automatically to the Oculus "Rift Audio" when `vr_enabled` is 1
