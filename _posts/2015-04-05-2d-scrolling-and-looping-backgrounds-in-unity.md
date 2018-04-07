---
id: 8
title: 2D Scrolling and Looping Backgrounds in Unity
date: 2015-04-05T06:30:00+00:00
author: Shah
layout: post
guid: http://hameid.net/2015/04/05/2d-scrolling-and-looping-backgrounds-in-unity/
permalink: /2d-scrolling-and-looping-backgrounds-in-unity/
categories:
  - Uncategorized
tags:
  - 2D Game
  - 'C#'
  - Code Snippet
  - Game Development
  - Programming
  - Unity 3D
---
Recently, I started to learn game development with Unity. So, I started working on a simple infinite side-scrolling game. For this, I searched online for various ways to scroll and loop the background.

Unfortunately, None worked for me, for some reasons. After playing around with Unity for sometime, I wrote my own script that could infinitely scroll and loop the background.

Here is what I did to get scrolling and looping backgrounds in Unity 3D.

  1. Drag and drop the background texture into the **Scene**. Make sure that the texture is wider than the target resolution.

  2. Select the background in the **Hierarchy** and look in the **Inspector**.

  3. Set the ‘X’ and ‘Y’ position to zero.

  4. Click on **“Add Component“** and select **“Physics 2D -> Rigidbody 2D“**

  5. Make sure that **“Is Kinematic“** is checked.

  6. Again, click on **“Add Component“** and Select **“New Script“**. Let the Name be **“BackgroundRepeater“** and Language be **C#**.

  7. Open the `BackgroundRepeater.cs` Script and paste the following code into it and save it.
    
    * * *
    
    **BackgroundRepeater.cs**
    
        using UnityEngine;
        using System.Collections;
        public class BackgroundRepeater : MonoBehaviour {
            public Vector2 velocity = new Vector2(-2, 0);
            private float spriteWidth;
            private Transform cameraTransform;
            void Start() {
                cameraTransform = Camera.main.transform;
                SpriteRenderer spriteRenderer = GetComponent() as SpriteRenderer;
                spriteWidth = spriteRenderer.sprite.bounds.size.x;
                GetComponent().velocity = velocity;
            }
            void Update() {
                if( ( transform.position.x + spriteWidth ) < cameraTransform.position.x ) {
                    Vector3 newPos = transform.position;
                    newPos.x += 2.0f * spriteWidth;
                    transform.position = newPos;
                }
            }
        }
        
    
    * * *

  8. Right click on background in **Hierarchy** and select **“Duplicate“**

  9. Select the duplicated background and set the **X** value of **Transform**‘s position such that the duplicated background will be placed immediately next to the original one.

 10. Play the scene and now you have your background scrolling and looping.

You can change the speed and direction from the script by changing the value of **Vector2** object `vector`.

I am still a beginner when it comes to Unity and I know there may be other efficient ways to scroll and loop backgrounds. I was just impatient that I wrote the script myself.