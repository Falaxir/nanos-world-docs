---
title: Characters Meshes
description: How to correctly import custom Models into nanos world
tags: [assets, characters, skeletal-meshes]
keywords: [mannequin, character, skeleton, mesh, unreal]
---


:::info

nanos world Characters use Unreal’s Default Mannequin Skeleton. So any Skeletal Mesh which uses it by default will probably work in nanos world as a [Character](/scripting-reference/classes/character.mdx).

:::

## Tips for integrating Skeletal Meshes with nanos world Character

### 1. Use nanos world Skeleton SKEL_Mannequin

It’s of paramount importance to convert all **Skeleton** references to use nanos world **Skeleton** instead, if the Skeletal Mesh you imported is 100% equal to UE4’s Mannequin Skeleton, this conversion won’t be even noticed, but if the Skeleton of the Skeletal Mesh you are importing have more bones or is different, it won’t work! You can try remake/modify it in a 3D software like Blender and make it equal to UE4’s Mannequin.

:::caution

**Note:** It is only possible to convert Skeletal Meshes of Meshes which already use the default **Unreal Mannequin Skeleton**.

:::

For that, just right click on your **Skeletal Mesh** ➡ Skeleton ➡ Assign Skeleton, and select our Skeleton `SKEL_Mannequin`, press _Accept_ to convert:  


#### Right click on your mesh and select to assign a Skeleton

![Right click on your mesh and select to assign a Skeleton](/img/docs/character-meshes-01.jpg)


#### Selecting SKEL_Mannequin and pressing Accept to convert

![Selecting SKEL_Mannequin and pressing Accept to convert](/img/docs/character-meshes-02.jpg)


### 2. Use nanos world Physics Assets PHYS_Mannequin

Besides converting your mesh to use nanos world **Skeleton**, it is also needed that you set your mesh to use the nanos world **Physics Assets**.

:::tip

This is needed so your Characters can have a proper in-game Ragdoll physics.

:::

Open your **Skeletal Mesh** and set the **Physics Asset** to use `PHYS_Mannequin`:


#### Opening Skeletal Mesh to use the proper Physics Asset

![Opening Skeletal Mesh to use the proper Physics Asset](/img/docs/character-meshes-03.jpg)


## Importing a new Character Skeletal Mesh

Learn how to import and use custom Skeletal Meshes in nanos world Characters.

For this Guide, we will import a Skeletal Mesh from [Stylized Character Kit: Casual 01](https://www.unrealengine.com/marketplace/en-US/product/stylized-male-character-kit-casual) \(which is a [Free Marketplace Content for September 2020](https://www.unrealengine.com/en-US/blog/featured-free-marketplace-content---september-2020)\). 


#### Stylized Character Kit from Unreal Engine Marketplace

![Stylized Character Kit from Unreal Engine Marketplace](/img/docs/character-meshes-04.jpg)

Also, we will be using our [Assets Development Kit - ADK](/assets-modding/creating-assets/adk-assets-development-kit.md), make sure you downloaded it.


### Downloading the Asset Pack from Unreal Marketplace

The first step is to download the Asset Pack _Stylized Character Kit: Casual 01_ from UE4 Marketplace, to do so, please follow:

1. _➡ Epic Games Launcher_
2. _➡ Unreal Engine_
3. _➡ Library_
4. ⬇ Scroll to _**VAULT**_ section

In Vault section you will find all your Marketplace content you have in your account, to download it click on _Add To Project_ and select the **Assets Development Kit** project, this will download all files and ‘install’ them into the ADK project.  


#### Finding Stylized Character Kit: Casual 01

![Finding Stylized Character Kit: Casual 01](/img/docs/character-meshes-05.jpg)


#### Adding Stylized Character Kit: Casual 01 to ADK Project

![Adding Stylized Character Kit: Casual 01 to ADK Project](/img/docs/character-meshes-06.jpg)

You can now notice that there is a new folder `Content/SCK_Casual01/` in the ADK project, this is the Asset Pack you just downloaded from UE4 Marketplace: 

![](/img/docs/character-meshes-07.jpg)

And you can find it’s Skeletal Meshes inside `Content/SCK_Casual01/Models/Premade_Characters/`: 


#### Opened Premade_Characters folder

![Opened Premade_Characters folder](/img/docs/character-meshes-08.jpg)


### Copying the wanted files to our Asset Pack folder

For this example, let’s import the Skeletal Mesh `MESH_PC_00` to nanos world and use it as our Character’s Mesh: 


#### Opened MESH_PC_00

![Opened MESH_PC_00](/img/docs/character-meshes-09.jpg)

The first step is to copy it and all it’s dependencies to your `AssetPack/` folder inside the Project:

:::info

If you want, you don’t need to do this and instead you can generate an Asset Pack with all files from the Marketplace, but will create a big and kind of useless content for nanos world.

:::

To do so, just drag-n-drop `MESH_PC_00` into your `AssetPack/` folder and select _Advanced Copy Here_, this will copy all files and all dependencies in there, i.e. only the real needed ones: 

#### Right clicked MESH_PC_00 and Advancing Copying into MyAssetPack/ folder

![Right clicked MESH_PC_00 and Advancing Copying into MyAssetPack/ folder](/img/docs/character-meshes-10.jpg)

Press OK to confirm: 


#### Confirming copying files

![Confirming copying files](/img/docs/character-meshes-11.jpg)

And now we have only our wanted Skeletal Mesh and it’s Textures/Materials into our Asset Pack folder, which we will export: 

#### All files copied automatically
![All files copied automatically](/img/docs/character-meshes-12.jpg)

### Converting the Skeleton to nanos world’s Skeleton and Physics Asset

:::info

Please refer to section [Tips for integrating Skeletal Meshes with nanos world Character](characters-meshes#tips-for-integrating-skeletal-meshs-with-nanos-world-character) for converting the `MESH_PC_00` to use our **Skeleton** and the **Physics Asset**.

:::

After it’s converted, save everything and you can delete the old Skeleton \(which was located at `SCK_Casual01/Mannquin/` folder\): 

#### Deleting old useless Skeleton
![Deleting old useless Skeleton](/img/docs/character-meshes-13.jpg)

### Exporting / Packaging / Cooking the Assets to nanos world

Cooking/Packaging Unreal Engine Projects is very straightforward \(this is the same as ‘generating’ your game’s .exe if you are making a game in UE4\).

Before we export it, let’s say to UE4 to only export our AssetPack folder, otherwise it will compile and export all folders in the Project. You can skip this step if you don’t care, but will increase the packaging time.

For that, open the Project Settings ➡ Packaging \(or search for _Directories to never Cook_\), and let’s add a blacklist of directories to skip cooking \(exporting\), I’m selecting the one from which we imported: `SCK_Casual01/` which we don’t want exported together because we had already copied the files we want to our AssetPack/ folder: 

#### Selecting which folders to Cook
![Selecting which folders to Cook](/img/docs/character-meshes-14.jpg)

And now we just need to Package the Project! File ➡ Package Project ➡ Windows \(64-bit\), and select a folder in your PC to save it: 

#### Packaging the Project
![Packaging the Project](/img/docs/character-meshes-15.jpg)

### Getting the Files & Generating Assets.toml

We are almost finished! Now, let’s copy all cooked files into our `Server/Assets/` folder! For that, find and open the folder which you just Packaged from UE4, you will have something like this: 

#### Packaged the Project
![Packaged the Project](/img/docs/character-meshes-16.jpg)

The folder we want is inside `Content/YourAssetFolder`: 

![](/img/docs/character-meshes-17.jpg)

Let’s copy it into our `Server/Assets/`: 

![](/img/docs/character-meshes-18.jpg)

And the last step is to generate an `Assets.toml` file! For our luck, the ADK comes with a [Tool](https://docs.nanos.world/modding/AssetsDevelopmentKit.html#assets-toml-generator-nanosworld-blueprints-utility-wbp-assetstomlgenerator) which generates an `Assets.toml` configuration automatically for us!

We just need to put the AssetPack/ folder name in there and press _GENERATE_: 

![](/img/docs/character-meshes-19.jpg)

Now you just need to create an `Assets.toml` file inside your `Server/Assets/MyAssetPack/` folder and paste the generated configuration inside of it: 

![](/img/docs/character-meshes-20.jpg)

### Using the Skeletal Mesh in a Character through Scripting

The last step is to use it! For that, you just need to use it’s Key `MyAssetPack::MESH_PC_00`! E.g.:

```lua title="Server/Index.lua"
local char = Character(Vector(0, 300, 100), Rotator(), "MyAssetPack::MESH_PC_00")
```

![](/img/docs/character-meshes-21.jpg)

:::tip

And… voila! Imported and integrated with all nanos world animations! 

:::

