---
id: 14
title: Animate HubTile With The Effect You Want
date: 2015-08-21T06:30:00+00:00
author: Shah
layout: post
guid: http://hameid.net/2015/08/21/animate-hubtile-with-the-effect-you-want/
permalink: /animate-hubtile-with-the-effect-you-want/
categories:
  - Uncategorized
tags:
  - 'C#'
  - HubTile
  - Windows 10
  - Windows Phone
  - Windows Phone Toolkit
  - XAML
---
HubTile is one of the many components that are a part of [Windows Phone Toolkit](https://phone.codeplex.com/) package. Basically, HubTile is an In-App Tile that can have Title, Message, Notification and Image.

A HubTile is animated with either **Flip** effect or **Translate** effect randomly. And, there is no direct way to choose with which effect a HubTile should be animated. But, that doesn’t mean you couldn’t customize it at all.

While developing the app for [Pointers 2K15](/tag/pointers-2k15/), I wanted a few HubTiles to have the **Flip** effect alone. After a few hours of messing up with the HubTile control, I came up with the following way to animate HubTile with the effect you want.

  1. Open **Visual Studio** and create a new **Blank App (Windows Phone)** project.

  2. Select **Project » Manage Nuget** Packages. Search for **“wptoolkit”** and install **Windows Phone Toolkit** from the search results.

  3. Double-click on `MainPage.xaml` from **Solution Explorer** and add a reference to the **Windows Phone Toolkit** by adding the following code just above the line `mc:Ignorable=”d”`.
    
    * * *
    
        xmlns:toolkit="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone.Controls.Toolkit"
        
    
    * * *

  4. Copy-Paste the following code inside the Grid named `LayoutRoot` to create two HubTile controls.
    
    * * *
    
        <StackPanel Grid.Row="1" Orientation="Horizontal">
            <toolkit:HubTile Title="Flip Tile" x:Name="flipTile" IsFrozen="True" Background="#1BA1E2" Source="Images/hameid.png" Message="This HubTile is animated only with 'Flip' Effect." Size="Medium" Margin="12,0,0,0" />
            <toolkit:HubTile Title="Translate Tile" x:Name="translateTile" IsFrozen="True" Background="#1BA1E2" Source="Images/hameid.png" Message="This HubTile is animated only with 'Translate' Effect." Size="Medium" Margin="12,0,0,0" />
        </StackPanel>
        
    
    * * *
    
    The first HubTile will be animated only with **“Flip”** Effect while the second one will be animated with **“Translate”** effect.
    
    You could see `IsFrozen` attribute of the HubTile controls are set to true in the above code. That’s because we don’t want HubTile to animate on its own.

  5. Now that HubTile is prevented from animating, We have to change the state of the HubTile for every fixed interval of time manually with code. For this purpose, We can use **DispatcherTimer**.
    
    And, To keep track of the current state of the HubTile controls, we can use **String** variables. Declare these **DispatcherTimer** objects and **String** variables as members of `MainPage` class.
    
    * * *
    
        private DispatcherTimer dT1, dT2;
        String sFlip = "Expanded", sTranslate = "Expanded";
        
    
    * * *
    
    The **String** variables are initialized with the initial state of the HubTile controls which is **“Expanded“**.

  6. Now, the **DispatcherTimer** objects have to be initialized. Also, the **“Tick”** event and an interval should be set. After that, the objects have to be triggered by calling the `Start()` method. Place the following piece of code inside your `MainPage` class’ constructor to do this.
    
    * * *
    
        dT1 = new System.Windows.Threading.DispatcherTimer();
        dT1.Tick += new EventHandler(dT1_Tick);
        dT1.Interval = new TimeSpan(0, 0, 0, 0, 3000);
        dT1.Start();
        
        
        dT2 = new System.Windows.Threading.DispatcherTimer();
        dT2.Tick += new EventHandler(dT2_Tick);
        dT2.Interval = new TimeSpan(0, 0, 0, 0, 3000);
        dT2.Start();
        
    
    * * *
    
    I have set the Interval such that the **“Tick”** event will be invoked for every 3000 ms (i.e. 3 seconds). You can change it according to your preference.
    
    Note that `dT1_Tick()` and `dT2_Tick()` are methods that handle the **DispatcherTimer** objects’ **“Tick”** event.

  7. Here comes the most important part of this tutorial. We have to define the `dT1_Tick()` and `dT2_Tick()` methods such that they switch the state of the corresponding HubTile control. The following code will do the trick for you.
    
    * * *
    
        private void dT1_Tick(object sender, EventArgs e)
        {
            switch (sFlip)
            {
                case "Expanded":
                    sFlip = "Flipped";
                    break;
                case "Flipped":
                    sFlip = "Expanded";
                    break;
            }
            VisualStateManager.GoToState(this.flipTile, sFlip, true);
        }
        
        
        private void dT2_Tick(object sender, EventArgs e)
        {
            switch (sTranslate)
            {
                case "Expanded":
                        sTranslate = "Semiexpanded";
                    break;
                case "Semiexpanded":
                    sTranslate = "Collapsed";
                    break;
                case "Collapsed":
                    sTranslate = "Expanded";
                    break;
            }   
            VisualStateManager.GoToState(this.translateTile, sTranslate, true);
        }
        
    
    * * *
    
    The above code just finds the next state of the HubTile and updates the **String** variables. Then, it changes the state of the HubTile by using the `GoToState()` method of **“VisualStateManager“**.

  8. Finally, We should stop the **DispatcherTimer** objects. Just call the `Stop()` in the `MainPage` class’ destructor to stop them.
    
    * * *
    
        dT1.Stop();
        dT2.Stop();
        
    
    * * *

  9. Now, Build and run the project. You can see that the first HubTile is animated only with **“Flip”** effect whereas the second HubTile is animated only with **“Translate”** effect.

While setting up the interval for the **DispatcherTimer** objects make sure that they are not the same. Otherwise, All HubTile controls changing state at the same time may look unrealistic.

If anyone is wandering, You can download the complete source code here at the [this link](https://adf.ly/1N5N0K).

Have a query or suggestion? Leave me a comment. I’d be happy to reply back.