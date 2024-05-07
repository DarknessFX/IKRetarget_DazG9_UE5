     .----------------.  .----------------.  .----------------. 
    | .--------------. || .--------------. || .--------------. |
    | |  ________    | || |  _________   | || |  ____  ____  | |
    | | |_   ___ `.  | || | |_   ___  |  | || | |_  _||_  _| | |
    | |   | |   `. \ | || |   | |_  \_|  | || |   \ \  / /   | |
    | |   | |    | | | || |   |  _|      | || |    > `' <    | |
    | |  _| |___.' / | || |  _| |_       | || |  _/ /'`\ \_  | |
    | | |________.'  | || | |_____|      | || | |____||____| | |
    | |              | || |              | || |              | |
    | '--------------' || '--------------' || '--------------' |
     '----------------'  '----------------'  '----------------' 

           DarknessFX @ https://dfx.lv | Twitter: @DrkFX

## About
Sample project with IKRig and IKRetarget assets to help retarget Daz3D Genesis 9 characteres to Unreal Engine 5.4.1 .

> [!NOTE]
> I'm not a Rigger or Character Artist, I'm sharing this project to help other gamedevs to simplify this process.<br/>
> Suggestions or contributions are welcome.

<sub>Ctrl+LeftClick 📷 for screenshots.</sub>

## Requirements
- Unreal Engine 5.4.1 (https://www.unrealengine.com/en-US/download)
- Daz 3D 4.22 (https://www.daz3d.com/technology/)<br/>
  Optional: Get free Daz packs from Daz Shop (https://www.daz3d.com/shop#filter_compat_figures=Genesis%209&filter_vendor=Daz%20Originals&order=price^-1&filtered=1)
- DazToUnreal Plugin (https://github.com/David-Vodhanel/DazToUnreal/releases)<br/>
  Note: Inside DazToUnreal.Zip plugin there is also an updated version of DazToUnreal Bridge in UE_5.4\DazToUnreal\Resource\dzunrealbridge.dll , I recommend to use this DLL version in Daz too.

## How To Use

- Download this project ([releases](https://github.com/DarknessFX/IKRetarget_DazG9_UE5/releases)), unzip and open in Unreal Engine.
- Add Feature or Content Pack ([📷](.git_img/how_AddTPSPack1.png)) > Third Person Template ([📷](.git_img/how_AddTPSPack2.png)).
- Open Content\ThirdPerson\Maps\ThirdPersonMap .<br/>
  Note: If the ThirdPersonMap map shows up completely blank, delete the PostProcessVolume.
- Delete Content\ThirdPerson\Characters folder, force delete if asked.
- Add [Control Rig Samples Pack](https://www.unrealengine.com/marketplace/en-US/product/control-rig-samples-pack) from Unreal Engine Marketplace/Epic Games Store to this project, overwrite files if asked.
- Optional: Check DazToUnreal Plugin settings ([📷](.git_img/00_DazToUnreal_Settings.png)).
- Open Daz Studio, empty scene, add Daz_Library\People\Genesis 9\Genesis 9 character.<br/>
  Optional: Add clothes from Daz_Library\People\Genesis 9\Clothing\Basic Clothes.
- **Rename the Character to Gen9 ([📷](.git_img/how_RenameChar.png)).**
- Click File > Send To > Daz To Unreal , configure the settings like the image ([📷](.git_img/01_DazToUnreal.png)) .
- In Unreal Engine, after importing from Daz, your Content\DazToUnreal\Gen9 folder shall have 5 files ([📷](.git_img/05_IKRetargeter_Created.png)).
- **Rename as show in the image ([📷](.git_img/05_IKRetargeter_Created.png))**: Skeleton = SK_Gen9 , Skeletal Mesh = SKM_Gen9 , Physical Asset = SPA_Gen9 .
- Go to Content\ControlRig\Characters\Mannequins\Animations folder, right-click ABP_Manny > Retarget Animations ([📷](.git_img/20_RetargetABP.png)).
- Select ([📷](.git_img/21_RetargetWnd.png)) : Source = SKM_Manny, Target = SKM_Gen9, Disable Auto Generate, Retarget = SRT_Gen9, chose all **Manny and MM** animations. Click Export Animations.
- Create a new folder at Content\DazToUnreal\Gen9\Animations ([📷](.git_img/22_RetargetNewFolder.png)).
- Add Manny in Search field and Gen9 in Replace field ([📷](.git_img/23_RetargetRename.png)).
- Click Export, then click Ok in the Batch Options window ([📷](.git_img/24_BatchOptions.png)).
- After exporting, click Save All.
- Delete ABP_Gen9_PostProcess.
- Open ABP_Gen9 > AnimGraph > Control Rig node:<br/>
  Replace Control Rig Class with SCR_Gen9_BasicFootIK ([📷](.git_img/25_ABP_CR.png)).<br/>
  Open Main States > Land node, link MM_Land directly to Output and disable Looping in Details panel ([📷](.git_img/26_ABP_FallLoop.png)).<br/>
  Open Main States > Jump node, select MM_Jump node and disable Looping in Details panel ([📷](.git_img/27_ABP_JumpLoop.png)).
- Open Content\ThirdPerson\Blueprints\BP_ThirdPersonCharacter, go to Viewport tab, Details panel: Change Skeletal Mesh to SKM_Gen9 and Anim Class to ABP_Gen9 ([📷](.git_img/28_BPThirdPerson.png)).
- Play ([📷](.git_img/29_Play.png))! 🍻👍

## IKRetarget Details

- Because Manny from ThirdPerson template have less info in the IKRig, I opted to use the more recent Manny from Control Rig Samples Pack [📷](.git_img/02_Manny_diff.png).<br/>
- I edited Manny IKRig (now renamed to Content\DazToUnreal\SIK_Manny) adding Pelvis and Neck chain targets, changed Head to just Head [📷](.git_img/03_SIK_Manny.png).<br/>
- After imported Daz character I use Create IK Retargeter with SKM_Manny source mesh [📷](.git_img/03_SIK_Manny.png).<br/>
- SIK_Gen9 edited: Sort Chains [📷](.git_img/06_SortChains.png), change Head chain from Neck1>Neck2>Head to just Head [📷](.git_img/07_HeadChain.png), add missing LeftHandIK chain [📷](.git_img/08_IKHandLChain.png) [📷](.git_img/09_IKHandLChainWnd.png), add Pelvis and Neck (Neck1>Neck2) chains [📷](.git_img/10_NeckAndHead.png).<br/>
- SRT_Gen9: Offset target X by 90 [📷](.git_img/11_OffsetTarget.png), check and set Chain Mappings with Head, Neck, Pelvis, LeftHandIK [📷](.git_img/12_LeftHandkIK.png), Reset All [📷](.git_img/14_ResetAll.png), Root > Align All Bones [📷](.git_img/15_AlignAllBones.png), Reset Feet [📷](.git_img/16_ResetFeet.png).<br/>
- Now because the spine, neck and head was bobbing, I made some small adjustments: Spine Rotation Alpha to 0.65 [📷](.git_img/17_SpineRotAlpha.png), Head Rotation Alpha to 0.5 [📷](.git_img/18_HeadRotAlpha.png), Neck disabled FK [📷](.git_img/19_HeadRotAlpha.png).<br/>

## Credits

Unreal Engine (https://www.unrealengine.com/en-US/download)<br/>
Daz 3D (https://www.daz3d.com/technology/)<br/>
David Vodhanel (https://github.com/David-Vodhanel/DazToUnreal/releases)<br/>
