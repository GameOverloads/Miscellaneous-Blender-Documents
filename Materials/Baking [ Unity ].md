BLENDER BAKING FOR UNITY
========================
BLENDER PRE-SETUP SETTINGS
--------------------------
### BLENDER PREFERENCES
- System
  - Cycles Render Devices

|  Driver Name  |   Recommended Driver Device     |
| :-----------: | :-----------------------------: |
| None          | Any Unsupported Render Device   |
| CUDA          | GTX Series Nvidia GPU           |
| OptiX         | RTX Series Nvidia GPU or Higher |
| HIP           | Vega AMD Series GPU or Higher   |
| oneAPI        | Intel Series GPU                |
> Select The Driver & Enable The Render Device Depending On Your System Hardware

### Scene Settings

| Setting Name  | Recommended Setting |
| :-----------: | :-----------------: |
| Render Engine |       Cycles        |
| Feature Set   |     Supported       |
|    Device     | CPU or GPU Compute  |
> Select CPU or GPU Compute Depending On Cycles Render Device Being Used

- Sampling
  - Render

|  Setting Name   | Recommended Setting |
| :-------------: | :-----------------: |
| Noise Threshold |  [ Enabled ]  .001  |
|   Max Samples   |          1          |
|   Min Samples   |          0          |

- Denoise [ Disabled ]

- Bake

|  Setting Name  | Recommended Setting |
| :------------: | :-----------------: |
|   Bake Type    |   Emit or Normal    |
> Pick Emit For Any Color or Data Map, or, Pick Normal For Normal Map Data

UNITY TEXTURE DATA NEEDED
-------------------------

|  Texture Name  |      Red / Green / Blue      |     Alpha    |
| :------------: | :--------------------------: | :----------: |
|     Albedo     |          Base Color          | Transparency |
|    Specular    |        Specular Color        |  Smoothness  |
|    Metallic    | Metallic / Occlusion / Blank |  Smoothness  |
|     Normal     |          Normal XYZ          |     Blank    |
|   Occlusion    | Metallic / Occlusion / Blank |  Smoothness  |
|    Emission    |        Emission Color        |     Blank    |
> Depending On Your Standard Shader Selected, Use Specular or Metallic
> Metallic & Occlusion Use The Same Mask Texture

STEP 1 - SET UP IMAGE TEXTURE NODE
----------------------------------

- Add Image Texture Node Nearby Material Shader Outputs & Material Output Node

- Create New Image From Image Texture Node
  - New Image Settings

|  Setting Name  | Recommended Setting  |
| :------------: | :------------------: |
|      Name      |         Bake         |
|      Width     | 1024 or 2048 or 4096 |
|      Height    | 1024 or 2048 or 4096 |
|      Alpha     |     [ Disabled ]     |
> Repeat This Step For As Many Materials Your Baking Out At Once That Are On Different UV Sets

STEP 2 - BAKE OUT MAP DATA
--------------------------

( Repeat For Each Material Being Baked Out )

- Connect Material Shader Output Needed To Material Output Node Surface Input
> Connect BSDF or Similar Output To Material Output Surface Input When Baking Out Normal

- Select Bake Image Texture Node [ Make Sure All Materials Have This Node Selected ]

( Change Bake Type Settings As Needed Before This Point )

- Go To Scene Settings
  - Bake
    - Tap Bake Button

STEP 2 - SAVE IMAGE DATA
------------------------

- Go To Image Editor

- Select Bake Image ( If Multiple Were Made, Repeat Below Steps )

- Image
  - Save As
    - Save As Settings

|  Setting Name  | Recommended Setting  |
| :------------: | :------------------: |
|  File Format   |      PNG or TGA      |
|     Color      |         RGB          |
|  Compression   |         0%           |
|  Color Space   |        sRGB          |

- Name As Needed

- Tap Save As Image
