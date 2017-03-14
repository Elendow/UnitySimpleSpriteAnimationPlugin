# Spritedow Animator
A plugin to do simple sprite animations avoiding the big and tedious Unitys's Mecanim system.
Oriented to programmers, if you prefer visual scripting you maybe prefer using Mecanim instead of this.

# Installation Guide
Simply copy the files on your project or use the UnityPackage included.

# Creating an animation
Use the animation editor to create new animation files. You can open it selecting **Sprite Animation Editor** on **Elendow Tools** tab.
- Give a name to the animation. This will be also the asset name. This name will be the one used to play the animations.
- Select the folder to save.
- Select the framerate of the animation.
- Add frames manually or dropping the sprite to the Drag&Drop box.
  - If you drop a Texture instead of a sprite to the Drag&Drop box, the plugin will take all the sprites on that Texture
  - You can change the duration of each frame, 1 by default, to any number greater than 0.
  - You can sort the frames.
- Any change is automatically saved.
- You can preview the animation.
  - The speed and loop settings of the preview window are only for that window.

# Inspector properties
- **Ignore TimeScale** will set the animation to ignore the game TimeScale.
- **Play on Awake** will start playing when the object awakes.
  - **One Shot** if false the animation will loop infinite times.
  - **Backwards** if true the animation will play backwards.
  - **Random Animation** if true the start animation will be random, and the animation will randomly change after every loop cicle.
  - **Start Animation** is the animation that will plays when **Play on Awake** is true.
- **Animations** is a list with all the animations.

# Using the animations
Add the **SpriteAnimator** or **UIAnimator** component to the object you want to animate and fill the animations list with the animations you want.
This component requires a SpriteRenderer or Image component to work. If the object doesn't have one, the animator will add it automatically.
On your code, use **GetComponent\<SpriteAnimator\>** or **GetComponent\<UIAnimator\>** to get the reference and start using it.

# Methods
- **Play (bool oneShot = false, bool backwards = false)** plays the first animation of the animation list.
- **Play (string animationName, bool oneShot = false, bool backwards = false)** plays the animation infinite times if oneShot = false, only one time if true, fordward if backwards = false and backwards if its true.
  * If the animation is the same that is playing, nothing will happend but the **oneShot** attribute will update.
  * If the animation is the same that was playing but its not playing now, the animation will **Reset** and **Resume** and the **oneShot** attribute will update.
  * If the animation is different, it will play the new animation from the start.
- **PlayRandom (bool playOneShot = false, bool backwards = false))** plays a random animation from the animation list.
- **Resume ()** resumes the current animation.
- **Stop ()** stops the current animation.
- **Reset ()** restarts the animation (playing or not) to its initial state. If the animation is not playing, the restart will be applied only when it start playing again.
- **SetActiveRenderer (bool active)** enable/disables the renderer.
- **FlipSpriteX (bool flip)** flips the sprite on the X axis.
  * Not working on UIAnimator yet.
- **AddCustomEvent (int frame)** adds an event to a specific frame of the first animation of the animation list and returns it.
- **AddCustomEvent (string animation, int frame)** adds an event to a specific frame of an animation and returns it.
  * If the animation name is empty, it will get the first animation of the list.
  * The event subscriber must have this estructure **MethodName(BaseAnimator caller){}**
- **GetCustomEvent (int frame)** returns the event of the first animation of the animation list at the specific frame. Returns null if there's no event on that frame and animation.
- **GetCustomEvent (string animation, int frame)** returns the event of the animation at the specific frame. Returns null if there's no event on that frame and animation.
  * If the animation name is empty, it will get the first animation of the list.

# Properties
- **IsPlaying { get; }** returns true if the animation is playing and false if not.
- **CurrentAnimation { get; }** returns a string with the current animation name.
- **DisableRenderOnFinish { set; }** sets the disableRenderer attribute. This will disable the renderer when the animation ends.
- **RandomAnimation { set; }** if true the animator will get a random animation after every loop cicle

# Events
- You can suscribe to the animation events using the AddListener(Listener) method of the UnityEvent class.
- **onFinish** calls when the animation reach the last frame.
- **onPlay** calls when the animation starts playing.
- **onStop** calls when the animation is forced to stop.
- You can add an event to a specific frame of an animation using the method **AddCustomEvent(string animation, int frame)**.
  * The event subscriber must have this estructure **MethodName(BaseAnimator caller){}**
  * Ex: animation.AddCustomEvent("Walk", 3).AddListener(StepFrame). Now on the frame 3 of the animation "Walk" the method StepFrame will be called.

# License
MIT
