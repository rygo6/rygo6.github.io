---
title: Unity Project Organization
layout: default
comments: true
---

# Unity Project Organization

Below is a description of the type of folder structure I use for Unity projects.

##### Asset Type Folders
You will see me refer to ``*Asset Type Folders*`` multiple times below. These are generic, repeated, folder names for each type of base asset.

```
*Asset Type Folders*
├── Animations
├── Materials
├── Models
├── Effects
├── Prefabs
├── Resources
├── Scripts
├── Shaders
├── Sounds
├── Substances
├── Textures
└── Prefabs
```

##### Project Folder Hierarchy
Listed below is an example layout of the Assets directory of an Unity project which categorizes content.

Categorization can help keep directories from becoming overcrowded and losing track of assets. It aids in keeping track of what asset belongs to what. The hope being you could delete the M1Abrams folder and not need to go hunting through the rest of the project to find all left over assets related to the M1Abrams. Or you could go in the M1Abrams folder, delete assets not currently being used by the M1Abrams, or make radical changes to assets in the M1Abrams folder, and be sure those changes will not negatively affect anything outside the folder.

Categorization should only be used when a category will house a substantial amount of assets for something relatively complex. For example, an M1Abrams will have multiple models, textures, scripts, prefab, particle effects, and animations. Thus an M1Abrams folder may be justified. Conversely a rock which would only have a model and a texture could live inside the Props category, with it's texture and model next to the multitude of other simple props. Melee weapons may not carry enough unique assets, nor complexity, thus they could potentially all share a Melee subcategory.

If categorization cannot be determined beforehand, then work in the base directory, or Common directory, until asset categorization can be determined. Then create an appropriate subfolder named for that categorization and move assets pertaining to that category there. If this is the first category subfolder you are creating, then you would create both a Common folder, and a category subfolder. Moving the appropriate assets to the category subfolder, and everything else to the Common folder.

An _ is placed before the Common directory name so that it is always placed at the top. Also an _ is placed before Project directory so it goes to the top of the list.

SourceAssets are the files created in Maya, Photoshop, Substance, etc. That are saved in their native format. You do not want Unity always reimporting these sources files, so keep them out of the Assets folder.

Below I list a ThirdParty folder and then also state third party libraries that cannot go in that folder should stay right below the Assets folder. This is because there are many third party assets which were not programmed in such a manner to enable them to exist anywhere else but under Assets. Typically they hardcoded a path assuming it will be directly under Assets. In these cases, you must leave them below Assets. It may also be a good idea to leave very complex third party packages directly under the Assets directory, as when you reimport an update to that package from the Asset Store, if you moved the files, it may not update it properly. Sadly most third party assets may not actually be best put in the ThirdParty folder.

An example of something which typically ends up in the ThirdParty folder in my project is something like the sqllite dll. It is a single file, I will manually be updating it myself and don't need to rely on the Unity package importer. Or the AWS plugin, as it is ideal to compile that yourself from source and you do not import it via the Unity package importer. Generally speaking, if you put things in the ThirdParty folder and don't let them import however they want to import on their own, you need to be able audit them yourself for being correct. You could just not have a ThirdParty folder and it would simplify this, but as stated, there are some third party assets which you know you can safely move around and manage yourself, then putting those in a ThirdParty can help consolidate your folder structure.

```
ProjectRoot
├── SourceAssets
│   ├── Maya
│   ├── SubstanceDesigner
│   └── Photoshop
├── Build
└── Assets
    ├── *MyCompanyName*
    │   ├── *Library Submodule from my company.*
    │   └── *Library Submodule from my company.*
    ├── *Third Party Libraries that cannot go in ThirdParty folder.*
    ├── ThirdParty
    │   └── *Any Third Party Library that can be moved here.*
    └── _Project
        ├── _Common
        │   └── *Asset Type Folders.*
        ├── Effects
        │   └── *Asset Type Folders.*
        ├── Level1
        │   └── *Asset Type Folders.*
        ├── Level2
        │   └── *Asset Type Folders.*
        ├── Props
        │   └── *Asset Type Folders.*
        ├── Vehicles
        │   ├── _Common
        │   │   └── *Asset Type Folders.*
        │   ├── Land
        │   │   ├── M1Abrams
        │   │   │   └── *Asset Type Folders.*
        │   │   └── HondaCivic
        │   │       └── *Asset Type Folders.*
        │   └── Air
        │       ├── SnowSpeeder
        │       │   └── *Asset Type Folders.*
        │       └── Volocopter
        │           └── *Asset Type Folders.*
        ├── Weapons
        │   ├── _Common
        │   │   └── *Asset Type Folders.*
        │   ├── Melee
        │   │   └── *Asset Type Folders.*
        │   └── Projectile
        │       └── *Asset Type Folders.*
        └── UI
            ├── _Common
            │   └── *Asset Type Folders.*
            ├── MainMenu
            │   └── *Asset Type Folders.*
            └── InGameMenu
                └── *Asset Type Folders.*
```

##### Tagging Rather than Hierarchy

Some might argue that categorizing things into so many folders is too much work or not worth it. Or that you could just rely on tags. I would agree with this for smaller projects. But if your project starts to become substantially large having 10,000 textures in a single folder can become a bit unwieldly. Especially if it is very easy to figure out categories. Perhaps something as basic as different folders for each level and one folder for all weapons, even something as simple as that will probably make your project folder less dauting to navigate.
