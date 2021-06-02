# Gravitrion
#### (originally Up and Down and All Around and before TMT_Gravity_Mod)
My attempt to port some code of this mod but make something different and maybe in 1.16.5

Change the direction of your gravity from downwards to upwards, north, east, south and west.

## Notes to other mod developers:

### Motion
A player's motion is considered relative to their current gravity direction. A Y motion of 1 while the player has Upwards gravity would result in the player moving downwards from the perspective of the world.

### Position
A player's position is for the most part unchanged, the only thing of note is that for N/E/S/W gravity directions is that the player's position is in the same place as their eye position. This is so that vanilla code that uses ```player.posY + player.getEyeHeight()``` doesn't need to be fixed using ASM. (in the future ```player.getEntityBoundingBox().minY + player.getEyeHeight()``` may also work, though currently does not)

### Hitboxes
This mod makes heavy use of its ```GravityAxisAlignedBB``` class in order to avoid massive changes to vanilla classes. If your mod requires you to use your own class that extends ```AxisAlignedBB``` for player hitboxes, then it is likely that your mod will never be compatible with this mod.

### ASM modifications
This mod uses ASM to modify the following classes (if your mod also modifies these classes then there will be a chance that your mod is not compatible with this mod, though it may be possible to fix):
- EntityPlayerMP
 - Superclass -> EntityPlayerWithGravity
- AbstractClientPlayer
 - Superclass -> EntityPlayerWithGravity
- EntityPlayerSP
 - onUpdateWalkingPlayer
 - onLivingUpdate
 - isHeadspaceFree
 - updateAutoJump
 - moveEntity
- NetHandlerPlayserver
 - processPlayer
 - processPlayerDigging
- NetHandlerPlayClient
 - handlePlayerPosLook
- Entity
 - moveEntity
 - moveRelative
- EntityLivingBase
 - moveEntityWithHeading
 - updateDistance
 - onUpdate
 - jump
- SoundManager
 - setListener
- RenderLivingBase
 - doRender
- EntityRenderer
 - getMouseOver
